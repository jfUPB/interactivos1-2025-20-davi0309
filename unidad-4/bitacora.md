# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/M_1_5_02)

Código a modificar:

``` js
// M_1_5_02
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * noise values (noise 2d) are used to animate a bunch of agents.
 *
 * KEYS
 * 1-2                 : switch noise mode
 * space               : new noise seed
 * backspace           : clear screen
 * s                   : save png
 */

'use strict';

var sketch = function(p) {
  var agents = [];
  var agentCount = 4000;
  var noiseScale = 300;
  var noiseStrength = 10;
  var overlayAlpha = 10;
  var agentAlpha = 90;
  var strokeWidth = 0.3;
  var drawMode = 1;

  p.setup = function() {
    p.createCanvas(p.windowWidth, p.windowHeight);

    for (var i = 0; i < agentCount; i++) {
      agents[i] = new Agent();
    }
  };

  p.draw = function() {
    p.fill(255, overlayAlpha);
    p.noStroke();
    p.rect(0, 0, p.width, p.height);

    // Draw agents
    p.stroke(0, agentAlpha);
    for (var i = 0; i < agentCount; i++) {
      if (drawMode == 1) agents[i].update1(noiseScale, noiseStrength, strokeWidth);
      else agents[i].update2(noiseScale, noiseStrength, strokeWidth);
    }
  };

  p.keyReleased = function() {
    if (p.key == 's' || p.key == 'S') p.saveCanvas(gd.timestamp(), 'png');
    if (p.key == '1') drawMode = 1;
    if (p.key == '2') drawMode = 2;
    if (p.key == ' ') {
      var newNoiseSeed = p.floor(p.random(10000));
      p.noiseSeed(newNoiseSeed);
    }
    if (p.keyCode == p.DELETE || p.keyCode == p.BACKSPACE) p.background(255);
  };
};

var myp5 = new p5(sketch);

```

[Enlace a la aplicación modificada](https://editor.p5js.org/)

Código modificado:

``` js
'use strict';

let agents = [];
let agentCount = 4000;


let noiseScale = 300;
let noiseStrength = 10;
let overlayAlpha = 10;
let agentAlpha = 90;
let strokeWidth = 0.3;
let drawMode = 1;


let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

// --- Estados de la app ---
const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAIT_MICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;

// --- Imagenes cargadas (ejemplo lineModule) ---



// --- Clase Agent ---
function Agent() {
  this.p = createVector(random(width), random(height));
  this.pOld = this.p.copy();
  this.stepSize = random(1, 5);

  this.update1 = function(noiseScale, noiseStrength, strokeWidth) {
    let angle = noise(this.p.x / noiseScale, this.p.y / noiseScale) * noiseStrength;
    this.p.x += cos(angle) * this.stepSize;
    this.p.y += sin(angle) * this.stepSize;

    strokeWeight(strokeWidth);
    line(this.pOld.x, this.pOld.y, this.p.x, this.p.y);

    this.pOld.set(this.p);

    if (this.p.x < 0 || this.p.x > width || this.p.y < 0 || this.p.y > height) {
      this.p.set(random(width), random(height));
      this.pOld.set(this.p);
    }
  };

  this.update2 = function(noiseScale, noiseStrength, strokeWidth) {
    let angle = noise(this.p.x / noiseScale, this.p.y / noiseScale, frameCount * 0.01) * noiseStrength;
    this.p.x += cos(angle) * this.stepSize;
    this.p.y += sin(angle) * this.stepSize;

    strokeWeight(strokeWidth);
    line(this.pOld.x, this.pOld.y, this.p.x, this.p.y);

    this.pOld.set(this.p);

    if (this.p.x < 0 || this.p.x > width || this.p.y < 0 || this.p.y > height) {
      this.p.set(random(width), random(height));
      this.pOld.set(this.p);
    }
  };
}

// --- Setup principal ---
function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);

  // Inicializar agentes
  for (let i = 0; i < agentCount; i++) {
    agents[i] = new Agent();
  }

  // Inicializar puerto serial
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(connectBtnClick);
}

// Aqui vamos a crear el boton para conectarnos con elmicrobit.
function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

// --- Draw ---
function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";

          // --- Mapear a parámetros ---
          noiseScale = map(microBitX, -1023, 1023, 100, 800);
          noiseStrength = map(microBitY, -1023, 1023, 1, 30);
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  }
function updateButtonStates(newAState, newBState) {
  
  if (newAState === false && prevmicroBitAState === true) {
    
    const newNoiseSeed = floor(random(10000));
    noiseSeed(newNoiseSeed);


    print("A pressed");
  }

  
  if (newBState === false && prevmicroBitBState === true) {
   
    saveCanvas('ImagenArte', 'png');


    print("B released");
  }

  // Actualizar estados previos
  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

  // --- Visualización ---
  fill(255, overlayAlpha);
  noStroke();
  rect(0, 0, width, height);

  stroke(0, agentAlpha);
  for (let i = 0; i < agentCount; i++) {
    if (drawMode == 1) agents[i].update1(noiseScale, noiseStrength, strokeWidth);
    else agents[i].update2(noiseScale, noiseStrength, strokeWidth);
  }
}


```

## Video

[Video demostratativo](URL)




