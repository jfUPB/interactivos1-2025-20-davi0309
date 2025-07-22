# Unidad 1

## 🛠 Fase: Apply

### Actividad 05

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
  connectBtn = createButton('Connect to micro:bit');
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
        x-=10;
      } else if (dataRx == "N") {
        x +=10;
      }
    }
  
  ellipseMode(CENTER);
        ellipse(x, y, 50, 50);
  fill(150,220,340,255)

        if (!port.opened()) {
            connectBtn.html("Connect to micro:bit");
        } else {
            connectBtn.html("Disconnect");
        }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
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

