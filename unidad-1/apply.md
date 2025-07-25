# Unidad 1

## 🛠 Fase: Apply

### Actividad 05
El sistema que creamos permite que, al presionar el botón A del micro:bit, se envíe una señal al computador a través del puerto. Esa señal luego es recibida por el programa hecho en p5.js que reacciona visualmente en la pantalla, cambiando el color a rojo de el cuadrado en pantalla como respuesta visual. Tambien usamos un sistema que evita enviar información constantemente desde el micro:bit y solo transmite datos únicamente si el micro:bit ya está conectado al programa del computador para que no se carguen muchos datos antes de dar click y la respuesta pueda ser mas rapida y eficiente.

### Actividad 06

[Mobimiento Circulo](https://editor.p5js.org/davi0309/sketches/Tk2h2VZmP)

Codigo del programa p5

``` js

let port;
let connectBtn;
let connectionInitialized = false;
let x = 200;
let y = 200;

function setup() {
  createCanvas(400, 400);
  background(220);
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) {
    let dataRx = port.read(1);
    if (dataRx == "A") {
      x -= 10;
    } else if (dataRx == "N") {
      x += 10;
    }
  }

  ellipseMode(CENTER);
  ellipse(x, y, 50, 50);
  fill(150, 220, 340, 255);

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  } else {
    connectBtn.html("Disconnect");
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}


```

``` py

from microbit import *

uart.init(baudrate=115200)
display.show(Image.MUSIC_QUAVER)

while True:
    if button_a.was_pressed():
        uart.write('A')
    if button_b.was_pressed():
        uart.write('N')

    sleep(100)
        
```

