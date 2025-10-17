
# Evidencias de la unidad 7

## Actividad 01

## Preguntas de entendimiento 

**¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?**

Esta es la URL que obtube https://pqfmh7rt-3000.use2.devtunnels.ms/, creo que necesitamos la otra URL por que como el nombre lo dice es local y por ende no se puede conectar a desde un celular que es completamente aparte ya que local es netamente interno, y la URL especifica es para identificarnos de los otros usuarios.

**Describe brevemente qué hace npm install y npm start**

Npm install, actualiza o descarga todas las dependencias que necesita mi proyecto y npm start, lo pone a correr y carga el servidor.

**¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?****

<img width="599" height="260" alt="imagen" src="https://github.com/user-attachments/assets/d6dd2d8d-60ab-4d7c-9c4c-9ea9a5cb3daa" />

No es diferente ya que manejan ek mismo servidor.

**Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?**

Esta aplicacion esta muy chevere ya que desde el cel puedo mover la pelota, lo que pasa es que si tiene un poco de delay en como se recibe los datos, y si funciono correctamente la interaccion.
Aqui se puede observar como se reciben los datos:

<img width="620" height="411" alt="imagen" src="https://github.com/user-attachments/assets/60a34c9c-dbbd-4b5e-b1bd-143b54a6a28c" />

## Actividad 02

**Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?**

Es un intermediario que sirve como puente para las conecciones en internet, se maneja de manera mucho mas segura y las respuestas del servidor tambien se conectan directamente con los clientes que se conecten deirectamente con la URL de Dev Tunnels, y este reenvía esa conexion de manera segura hacia el servidor local de Node.js

**Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.**

TouchMoved() es una función que se ejecuta automáticamente en un dispositivo con pantalla táctil cada vez que el usuario mueve un dedo en la pantalla sin levantarlo ya que tambien existe touchStarted(), touchEnded() por lo que este tipo de Touch me sirve solo cuando se esta presionando constantemente la pantalla sin levantarlo. Es equivalente a mouseDragged() en un computador con ratón, pero adaptado para pantallas táctiles.
y el threshold es una variable usada para limitar o filtrar la sensibilidad del movimiento, especialmente en celulares no tanto en mouse, ya que depronto el dedo tiembla o se generan movimientos involuntarios que no queremos cargar.


**Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?**

las ventajas de Dev Tunnels son:
> - sirve para conecciones en la msima red local.
> - se puede conectar remotamente aunque no esten en la misma red.
> - se genera un HTTPS automatico.
> - aunque esten los clientes en distintas redes se mantiene la compatibilidad y el flujo.

las desventajas de Dev Tunnels son:
> - Requiere una herramienta como visual code.

las ventajas de IP local son:
> - Funciona para conectarse ne la misma red local.
> - No necesita de una app externa.


las desventajas de IP local son:
> - No se puede conectar, si estan afuera de la red.
> - toca crear el HTTPS.
> - No tiene estabilidad en distintas redes.



**Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).**

Desde mi pc:
<img width="1919" height="916" alt="imagen" src="https://github.com/user-attachments/assets/75c8825d-cfd2-40a1-8d52-ec48115c5236" />

Desde el cel:
![Sin título](https://github.com/user-attachments/assets/847fe341-c86c-45d0-9f50-1c1f00766242)

Si lo muevo es asi el resultado:

<img width="1919" height="971" alt="imagen" src="https://github.com/user-attachments/assets/538e41ee-946a-417f-a619-a29c7460e7d6" />


## Actividad 03

**¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?**

Funciona para que las direcciones queden enviadas hacia la carpeta public y no tener que generar rutas especificas para cada parte de la carpeta, lo que permite que si se piden datos el servidor sepa donde buscarla ya que el control es automatico, en cambio si usamos el app.get(‘/ruta’, …), tenemos o toca definir las rutas especificas y colocar mas codigo por cada cosa que se pida en las carpetas. En la unidad anterior cada página hacía la solicitud de las bibliotecas necesarias que estaban ubicadas en la carpeta public.

**Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?**

Ps la funcion que se encarga de enviar desde ek movil es esta funcion que se encuentra en `/public/mobile`: 
```cpp
function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', touchData);

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}
```
esta funcion es la encargada de enviar la informacion si el usuario toca la pantalla con el dedo o con el mouse, y en el primer if que est este `if (socket && socket.connected)` se verifica si hay una conexion activa, si la hay se corre eso si no, no pasa nada, luego calcula la posicion y la envia por medio de `socket.emit('message', touchData);`.

El evento que recibe del servidor es aqui:

```cpp
socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });
```
y lo que hace es recibir el mensaje, luego lo muestra en la consola y por ultimo con `socket.broadcast.emit('message', message);` reenvia este mensaje a todos los clientes conectados.

**Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?**

Como vimos anterior mente el mensaje se envia a todos los clientes conectados, y ambos se actualizan.

**¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?**

El servidor muestra en la consola cuatro tipos de mensajes diferentes: uno indica el puerto de conexión, y los otros tres son respuestas a las acciones de los clientes.
Cuando un cliente se conecta o se desconecta, el servidor lo notifica con un mensaje específico, pero el registro que más aparece es el "Received message =>".
Los mensajes en la consola tienen este formato:

```cpp
Server is listening on http://localhost:3000
New client connected
Received message => { type: 'touch', x: 129, y: 213 }
Client disconnected
```

El mensaje "Received message =>" incluye las coordenadas del toque que realiza el usuario, las cuales se utilizan para que la ruta /desktop actualice la posición del círculo que aparece en pantalla.

## Actividad 04

Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.

<img width="917" height="611" alt="imagen" src="https://github.com/user-attachments/assets/72bdab14-8612-48bf-9394-e60625096e54" />


### Paso a paso

1. El usuario toca en el celular por ejemplo una direccion en pantalla asi `x=150, y=300`.
2. `touchMoved()` envía `type:'touch', x:150, y:300` al servidor con `socket.emit('message', touchData)`.
3. El servidor recibe el evento con el `socked.on` y lo envia con el `socket.broadcast.emit('message', message);`a los otros clientes por medio de esta funcion:
```cpp
socket.on('message', (message) => {
    console.log('Received message =>', message);
    socket.broadcast.emit('message', message);
});

```
5. De esta manera muestra el mensaje y lo difunde a los otros clientes.
6. El escritorio recibe los datos con el `socket.on('message', (data))` por medio de esta funcion:
```cpp
socket.on('message', (data) => {
    if (data.type === 'touch') {
        circleX = data.x;
        circleY = data.y;
    }
});

```
7. Se mueve ek circula a la direccion (150, 300) en el canva.
8. el proceso se repite con cada touch o movimiento que hagamos con el dedo


# Apply actividad 05

Bueno la idea de diseño que tengo es que cuando coloque una cancion se pueda ver una onda como si fuera el ecualizador de una cancion, y que mediante el touch se pueda acelerar o desacelerar la cancion y subir o bajar el pitch que este tenga como que tan grave o aguda es la cancion, ademas tambien planeo agregarle unos circulos que palpiten con el ritmo de los bajos o algo parecido.

> Cuando comence a preguntarle a chat se me ocurrio una idea mientras veia la documentacion de p5 y si uso el sistema de smoke que encontre en un ejemplo y le digo a chat que lo implemente en las bolitas para que si el dedo esta mas abajo de la pantalla este se aumente generando una sensacion de que estan como humito que dejan los circulos al moverse. [link de la documentacion de p5](https://p5js.org/examples/math-and-physics-smoke-particle-system/).

Ahora tambien me gusto agregarle color a la onda y una posicion centrada en el canva ya que lo primero que me paso chat no tenia nada que ver con lo que queria que se viera.

Tambien le dije que cuando moviera el dedo de arriba a abajo cambiara de color la onda
Esa fue mi idea de diseño.

Ahora lo que pudo lograr gpt con unos cuantos prompts de arreglo y demas para que funcionara debidamente y como se pedia es esto:

<img width="1917" height="896" alt="imagen" src="https://github.com/user-attachments/assets/a56e8cb0-1676-4368-93f2-38164c97415b" />


<img width="1910" height="895" alt="imagen" src="https://github.com/user-attachments/assets/dcaab5a8-f1e0-4258-871a-d4bb4a795d74" />




Ahora compartire los codigos:



### Desktop (sketch) :




```js
let socket;
let song;
let fft;
let playing = false;
let colorTone = [255, 0, 0];
let playbackRate = 1;
let pitch = 1;
let particles = [];
const port = 3000;

function preload() {
  song = loadSound('song2.mp3');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);
  fft = new p5.FFT();
  socket = io();

  socket.on('connect', () => {
    console.log('Conectado al servidor');
  });

  socket.on('message', (data) => {
    if (data && data.type === 'touch') {
      let normX = data.x / 300;
      let normY = data.y / 400;

      playbackRate = map(normX, 0, 1, 0.5, 2);
      song.rate(playbackRate);

      pitch = map(normY, 0, 1, 0.5, 2); // controla transición visual

      if (pitch < 1) {
        colorTone = [map(pitch, 0.5, 1, 255, 100), 50, 50];
      } else {
        colorTone = [50, 100, map(pitch, 1, 2, 100, 255)];
      }
    }
  });
}

function draw() {
  background(0, 80);

  if (playing) {
    let spectrum = fft.analyze();
    let bass = fft.getEnergy("bass");

    // ----- ONDA CENTRAL -----
    noFill();
    stroke(colorTone[0], colorTone[1], colorTone[2]);
    strokeWeight(2);
    beginShape();
    for (let i = 0; i < spectrum.length * 0.9; i += 6) { 
        let x = map(i, 0, spectrum.length * 0.9, 0, width);
        let y = height / 2 + map(spectrum[i], 0, 255, 100, -100);
        curveVertex(x, y);
    }   
    endShape();

    // ----- PARTÍCULAS DEL BAJO -----
    if (bass > 180 && particles.length < 120) {
      for (let i = 0; i < 6; i++) {
        particles.push(new Particle(random(width), random(height)));
      }
    }

    // Actualizar partículas
    for (let i = particles.length - 1; i >= 0; i--) {
      particles[i].update(bass, pitch);
      particles[i].display(pitch);
      if (particles[i].alpha <= 0) {
        particles.splice(i, 1);
      }
    }
  }
}

function mousePressed() {
  if (!playing) {
    song.loop();
    playing = true;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

// ----- CLASE DE PARTÍCULA -----
class Particle {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.baseSize = random(3, 6);
    this.size = this.baseSize;
    this.alpha = 180;
    this.life = random(60, 120);
    this.xSpeed = random(-1, 1);
    this.ySpeed = random(-1, 1);
    this.pulsePhase = random(TWO_PI); // para que no palpiten sincronizadas
  }

  update(bass, pitch) {
    // Transición de humo suave (de 0 a 1)
    let smokeIntensity = constrain(map(pitch, 1, 2, 0, 1), 0, 1);

    // Movimiento más flotante cuanto más humo haya
    this.x += this.xSpeed * (1 + smokeIntensity * 1.3);
    this.y += this.ySpeed * (1 + smokeIntensity * 1.3);

    // Efecto de “palpitar” amplificado
    // base en energía de bajo + oscilación rítmica independiente
    let pulseBase = map(bass, 100, 255, 0.9, 3.5);
    let pulseWave = sin(frameCount * 0.2 + this.pulsePhase) * 0.3 + 1;
    this.size = this.baseSize * pulseBase * pulseWave * (1 + smokeIntensity * 0.8);

    // Desvanecerse más lento si hay humo denso (más etéreo)
    this.alpha -= 1 + smokeIntensity * 0.7;
    this.life--;
  }

  display(pitch) {
    let smokeIntensity = constrain(map(pitch, 1, 2, 0, 1), 0, 1);
    noStroke();

    // Colores dinámicos tipo disco
    let t = frameCount * 0.04 + this.x * 0.02 + this.y * 0.02;
    let r = sin(t) * 127 + 128;
    let g = sin(t + TWO_PI / 3) * 127 + 128;
    let b = sin(t + (2 * TWO_PI) / 3) * 127 + 128;

    // Efecto de brillo con humo colorido
    let diffuse = lerp(0, 20, smokeIntensity);
    let alphaAdjusted = this.alpha * (1 - smokeIntensity * 0.1);

    // centro brillante
    fill(r, g, b, alphaAdjusted);
    ellipse(this.x, this.y, this.size + diffuse);

    // capas de humo suaves
    if (smokeIntensity > 0.1) {
      for (let i = 0; i < 3; i++) {
        fill(r, g, b, alphaAdjusted * 0.25);
        ellipse(
          this.x + random(-diffuse, diffuse),
          this.y + random(-diffuse, diffuse),
          this.size * (1.3 + smokeIntensity)
        );
      }
    }
  }
}
```

### mobile (sketch) en estas lineas de codigo fu mas cambiar un poco el canva para que se entendiera un poco mas la funcionalidad al cliente mobil:



```js
let socket;
let lastTouchX = null; 
let lastTouchY = null; 
const threshold = 5;

function setup() {
    createCanvas(400, 500);
    background(220);
    socket = io();

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
    });

    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });
}

function draw() {
    background(0);

  // Textos fijos en los bordes
  textSize(18);
  fill(100);
  text("Más tranquilo (bolas) ↑", width - 280, 40);
  text("Más ruidoso (bolas) ↓", width - 280, height - 40);
  text("→ Más rápido ", width - 130, height / 2);
  text("Más lento  ←", 10, height / 2);

  // Texto dinámico según el movimiento
  fill(255, 180);
  textSize(28);
  text(directionText, width / 2, height / 2);
}

function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', touchData);

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}
```
*Y en el servidor no movi nada pero igual lo coloco:*

### server.js:

```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

Explicacion breve:

```js
function preload() {
  song = loadSound('song2.mp3');
}
```

Esta parte del codigo se encarga de cargar el audio que tenemos en la carpeta de desktop.

En setup tenemos esta parte de codigo:

```js
fft = new p5.FFT();
socket = io();
```

para que sirven estas dos lineas. ps `fft = new p5.FFT()` crea el analizador que te devolverá el spectrum (arreglo de energía por banda) y getEnergy("bass") y `socket = io()` inicializa Socket.IO en el cliente (usa /socket.io/socket.io.js servido por el servidor).


En esta parte esta la logica que se encarga de leer el mensaje enviado por el touch:

```js
socket.on('message', (data) => {
  if (data && data.type === 'touch') {
    let normX = data.x / 300;
    let normY = data.y / 400;

    playbackRate = map(normX, 0, 1, 0.5, 2);
    song.rate(playbackRate);

    pitch = map(normY, 0, 1, 0.5, 2);

    if (pitch < 1) {
      colorTone = [map(pitch, 0.5, 1, 255, 100), 50, 50];
    } else {
      colorTone = [50, 100, map(pitch, 1, 2, 100, 255)];
    }
  }
});
```

y la parte del colorTone se encarga de cambiar el color segun donde enten los datos recibidos cambiando la paleta de color.

La onda central se crea en esta parte:
```js
let spectrum = fft.analyze(); // arreglo [0..255]
beginShape();
for (let i = 0; i < spectrum.length * 0.9; i += 6) {
  let x = map(i, 0, spectrum.length * 0.9, 0, width);
  let y = height / 2 + map(spectrum[i], 0, 255, 100, -100);
  curveVertex(x, y);
}
endShape();
```
Donde `fft.analyze()` devuelve un arreglo de amplitudes por banda (0–255) y i += 6 reduce la densidad de puntos (balance detalle/suavidad). El resto de codigo es para que la curva se vea mas suave o mas redonda en tal caso.

### Ahora todo lo que es deteccion de bajo s y generacion de particulas esta aqui:

**Primero los bajos:**

```js
let bass = fft.getEnergy("bass");
if (bass > 180 && particles.length < 120) {
  for (let i = 0; i < 6; i++) { particles.push(new Particle(random(width), random(height))); }
}
```

y lo que es la generacion de particulas va aqui:

```js
for (let i = particles.length - 1; i >= 0; i--) {
  particles[i].update(bass, pitch);
  particles[i].display(pitch);
  if (particles[i].alpha <= 0) particles.splice(i, 1);
}
```
Luego hay mas codigo que se encarga de actualizar las particulas y las ondas y luego tenemos el display que es esta parte de codigo:

```js
let smokeIntensity = constrain(map(pitch,1,2,0,1),0,1);
noStroke();
let t = frameCount * 0.04 + this.x * 0.02 + this.y * 0.02;
let r = sin(t) * 127 + 128;  // R,G,B ciclo
...
let diffuse = lerp(0, 20, smokeIntensity);
let alphaAdjusted = this.alpha * (1 - smokeIntensity * 0.1);
fill(r,g,b,alphaAdjusted);
ellipse(this.x, this.y, this.size + diffuse);

if (smokeIntensity > 0.1) {
  for (let i = 0; i < 3; i++) {
    fill(r,g,b,alphaAdjusted * 0.25);
    ellipse(this.x + random(-diffuse, diffuse), this.y + random(-diffuse, diffuse), this.size * (1.3 + smokeIntensity));
  }
}
```

**Y no se nos puede olvidar lo que hace que palpiten las particulas:**

- El factor pulseBase mapea bass a un rango amplio (0.9 → 3.5). Eso significa que con bajos fuertes la escala se multiplica varias veces sobre baseSize.
  
- pulseWave da una modulación temporal (oscilación), y pulsePhase hace que partículas no palpite en sincronía total.
  
- Al combinar ambos, el pulso es fuertemente perceptible: el tamaño sube rápidamente con cada golpe bajo y vuelve a bajar.























