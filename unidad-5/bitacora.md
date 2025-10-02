
# Evidencias de la unidad 5

## Actividad 03

### Preguntas de la Unidad:

**Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.**

Por que al enviar valores en ASCII no tenemos como saber que byte corresponde a cada valor por que estan juntos y toca separarlos o leer los con delimitadores como ( `,` y `n\`) para saber hasta donde llegan los bytes de cada dato y cuando se acaba la linea, en cambio con el nuevo protocolo y enviando los datos en binario, ya estamos delimitando cuandos bytes tiene cada dato, con esta linea `struct.pack('>2h2B')`.

**Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?**

Lo mas evident es que ya no estan las lineas de codigo que me ayudaban a leer por ejemplo el `n\` o el splitter que teniamos antes ahora solo le decimos que llegan 6 bytes, y que me lean 6 bytes y luego segun la posicion de estos bytes se les asigna a las 4 variables que tenemos. Por ejemplo en `microBitX = view.getInt16(0);` lo que entendemos es que al ser un int16 consume 2 espacios de bytes y el (0) se refiere desde donde comienza.

**¿Qué ves en la consola? ¿Por qué crees que se produce este error?**

Lo que se logra ver es que hay un error o un desface en como estan llegando los datos :
Buena linea:`microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false`
Mala linea:`92 microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false`


### Preguntas de analizis y comprension:

```js
let serialBuffer = []; // Buffer para almacenar bytes recibidos

let c;
let lineModuleSize = 0;
let angle = 0;
let angleSpeed = 1;
const lineModule = [];
let lineModuleIndex = 0;
let clickPosX = 0;
let clickPosY = 0;

function preload() {
  lineModule[1] = loadImage("02.svg");
  lineModule[2] = loadImage("03.svg");
  lineModule[3] = loadImage("04.svg");
  lineModule[4] = loadImage("05.svg");
}

let port;
let connectBtn;
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  // Generar eventos de keypressed
  if (newAState === true && prevmicroBitAState === false) {
    // create a new random color and line length
    lineModuleSize = random(50, 160);
    // remember click position
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }
  // Generar eventos de key released
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

function readSerialData() {
  // Acumula los bytes recibidos en el buffer
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  // Procesa el buffer mientras tenga al menos 8 bytes (tamaño de un paquete)
  while (serialBuffer.length >= 8) {
    // Busca el header (0xAA)
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); // Descarta bytes hasta encontrar el header
      continue;
    }

    // Si hay menos de 8 bytes, espera a que llegue el paquete completo
    if (serialBuffer.length < 8) break;

    // Extrae los 8 bytes del paquete
    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8); // Elimina el paquete procesado del buffer

    // Separa datos y checksum
    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    // Calcula el checksum sumando los datos y aplicando módulo 256
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue; // Descarta el paquete si el checksum no es válido
    }

    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0);
    microBitY = view.getInt16(2);
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    console.log(
      `microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState}`
    );
  }
}

function draw() {
  //******************************************
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
  }

  //*******************************************

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      // No puede comenzar a dibujar hasta que no se conecte el microbit
      // evento 1:
      if (microBitConnected === true) {
        // Preparo todo para el estado en el próximo frame
        print("Microbit ready to draw");
        strokeWeight(0.75);
        c = color(181, 157, 0);
        noCursor();
        port.clear();
        prevmicroBitAState = false;
        prevmicroBitBState = false;
        appState = STATES.RUNNING;
      }

      break;

    case STATES.RUNNING:
      // EVENTO: estado de conexión del microbit
      if (microBitConnected === false) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
        break;
      }

      //EVENTO: recepción de datos seriales del micro:bit

      readSerialData();

      if (microBitAState === true) {
        let x = microBitX;
        let y = microBitY;

        if (keyIsPressed && keyCode === SHIFT) {
          if (abs(clickPosX - x) > abs(clickPosY - y)) {
            y = clickPosY;
          } else {
            x = clickPosX;
          }
        }

        push();
        translate(x, y);
        rotate(radians(angle));
        if (lineModuleIndex != 0) {
          tint(c);
          image(
            lineModule[lineModuleIndex],
            0,
            0,
            lineModuleSize,
            lineModuleSize
          );
        } else {
          stroke(c);
          line(0, 0, lineModuleSize, lineModuleSize);
        }
        angle += angleSpeed;
        pop();
      }

      break;
  }
}

function keyPressed() {
  if (keyCode === UP_ARROW) lineModuleSize += 5;
  if (keyCode === DOWN_ARROW) lineModuleSize -= 5;
  if (keyCode === LEFT_ARROW) angleSpeed -= 0.5;
  if (keyCode === RIGHT_ARROW) angleSpeed += 0.5;
}

function keyReleased() {
  if (key === "s" || key === "S") {
    let ts =
      year() +
      nf(month(), 2) +
      nf(day(), 2) +
      "_" +
      nf(hour(), 2) +
      nf(minute(), 2) +
      nf(second(), 2);
    saveCanvas(ts, "png");
  }
  if (keyCode === DELETE || keyCode === BACKSPACE) background(255);

  // reverse direction and mirror angle
  if (key === "d" || key === "D") {
    angle += 180;
    angleSpeed *= -1;
  }

  // default colors from 1 to 4
  if (key === "1") c = color(181, 157, 0);
  if (key === "2") c = color(0, 130, 164);
  if (key === "3") c = color(87, 35, 129);
  if (key === "4") c = color(197, 0, 123);

  // load svg for line module
  if (key === "5") lineModuleIndex = 0;
  if (key === "6") lineModuleIndex = 1;
  if (key === "7") lineModuleIndex = 2;
  if (key === "8") lineModuleIndex = 3;
  if (key === "9") lineModuleIndex = 4;
}
```
***Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?***

- Al comienzo antes de conectar el micro.bit: Nada
- Cuando se conecta el micro.bit: Microbit ready to draw
- Cada vez que llegan datos válidos del micro.bit: microBitX: 123 microBitY: -45 microBitAState: false microBitBState: true
microBitX: 127 microBitY: -42 microBitAState: true microBitBState: true

- Presionando A en el micro.bit: A pressed
- Soltando B en el micro.bit: B released
- Si los paquetes llegan con error en checksum: Checksum error in packet

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Nota

| Criterio | Calificación | Justificación |
| --- | --- | --- |
| 1.**Profundidad de la indagación** | 4.7 / 5.0 | Comparé ASCII vs binario, expliqué framing, checksum y `struct.pack`. Mostré por qué antes necesitábamos delimitadores y ahora no. Faltó ampliar escenarios de uso . Podría mejorar con más escenarios de aplicación o ver lo del rendimiento. |
| **2. Calidad de la experimentación** | 4.3 / 5.0 | Probé cambios de orden. Funcionó el checksum y se vio el error de desface en consola. Faltó más medición y variaciones por que algunos eran bastante simples. |
| **3. Análisis y reflexión** | 4.6 / 5.0 | Analicé errores de sincronización y el rol del header y checksum. Expliqué bien el desfase en los paquetes y lo que aparece en consola. |
| **4. Apropiación y articulación de conceptos** | 4.5 / 5.0 | Usé conceptos técnicos (framing, checksum, `struct.pack`, `DataView`) y mostré cómo se conectan. La verdad pude explicarlos mejor con ejemplos visuales. |

**La nota final es:** 4.5 me sirvio mucho realizar el analisis y reflexion y las preguntas de indagacion aunque no estuve del todo bien con los experimentos que queria plantear.





