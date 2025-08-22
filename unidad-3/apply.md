# Unidad 3


## 🛠 Fase: Apply
### Actividad 06
Codigo funcional de la bomba 2.0 en p5.js
```js



let validChars = "ABST";


let count = 20;
let PASSWORD = ["A", "B", "A"];
let llave = [" ", " ", " "];
let keyIndex = 0;
let State = "CONFIG";


function setup() {
  createCanvas(400, 400);
  textAlign(CENTER,CENTER)
  background(220);
  startTime = millis();
 
  
}

function draw() {
  background(220);
 

  textSize(20);
  text("Presiona A, B, S o T", width / 2, height - height / 3);
  BombTask()
 
   if (State === "ARMED") {
    let uTime = millis();
    if (uTime - startTime > 1000) {
      startTime = uTime;
      count--;
      if (count <= 0) {
        State = "EXPLODED";
      }
    }
   }
  if (State === "CONFIG"){
     text(count, width / 2, height / 2);
   }
   else if (State === "ARMED"){
     if (count > 0){
       text(count, width / 2, height / 2);
     }     
   }
   if (State === "EXPLODED"){
     text("exploto", width / 2, height / 2);
     text("Presiona T para reiniciar", width / 2, height / 3);
   }



  
}

function keyPressed() {
  let keyValue = key.toUpperCase();
  if(validChars.includes(keyValue)){
    BombTask(keyValue);
 
    
  }

}
function BombTask(keyValue) {
  if (State === "CONFIG") {
    if (keyValue === "A") {
      count = max(10, count + 1);
      } 
    else if (keyValue === "B") {
      count = max(10, count - 1);
    } 
    else if (keyValue === "S") {
      startTime = millis();
      State = "ARMED";
    } 
  }
  else if (State === "ARMED"){
    if (keyValue === "A" || keyValue === "B") {
      llave[keyIndex] = keyValue;
      keyIndex++;
    }
  }
  if (keyIndex === llave.length){
    let passIsOk = true
    for (let i = 0; i < llave.length; i++){
      if(llave[i] !== PASSWORD[i] ){
        passIsOk = false
        break;
      }
    }
    if (passIsOk === true){
      count = 20;
      keyIndex = 0;
      State = "CONFIG";
    }
    else{
      keyIndex = 0;
    }
  }
  else if (State === "EXPLODED") {
    if (keyValue === "T") {
      count = 20;
      startTime = millis();
      State = "CONFIG";
    }
  }
}
```
### Actividad 07
este fue el codigo que pense que quedaria mejor de los que utilizamos en el curso para este ejercicio en la parte del microbit ya que me ayuda a enviar por el puero mediante el uart las teclas que se presionan o en si los inputs que genera el microbit.
```py
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('S')  # Shake envía 'S' (para armar)
        sleep(500)
    if pin_logo.is_touched():
        uart.write('T')  # Touch envía 'T' (para reiniciar)
        sleep(500)
```

y este es mi codigo de p5 no esta completo, por que siento que se tiene que hacer con prueba y error y como el la casa no tenia microbit esto fue lo maximo que pude hacer sin poder validar si lo que estaba haciendo estaba correcto, lo que hice fue que el ehercicio 06 le agregue unos botones para que se conectara con el micro.bitt y abriera el puerto serial. Aun me falta colocar los inputs como eventos genericos para que se pueda validar de la misma forma asi en teclado o en botones de microbit.
```js


let validChars = "ABST";


let count = 20;
let PASSWORD = ["A", "B", "A"];
let llave = [" ", " ", " "];
let keyIndex = 0;
let State = "CONFIG";
let port;
let connectBtn;
let connectionInitialized = false;


function setup() {
  createCanvas(400, 400);
  textAlign(CENTER,CENTER)
  background(220);
  startTime = millis();
  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(80, 300);
  connectBtn.mousePressed(connectBtnClick);
 
  
}

function draw() {
  background(220);
 

  textSize(20);
  text("Presiona A, B, S o T", width / 2, height - height / 3);
  BombTask()
  
  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
  }   
  else {
    connectBtn.html("Disconnect");
  }

 
  if (State === "ARMED") {
    let uTime = millis();
    if (uTime - startTime > 1000) {
      startTime = uTime;
      count--;
      if (count <= 0) {
        State = "EXPLODED";
      }
    }
   }
  if (State === "CONFIG"){
     text(count, width / 2, height / 2);
   }
   else if (State === "ARMED"){
     if (count > 0){
       text(count, width / 2, height / 2);
     }     
   }
   if (State === "EXPLODED"){
     text("exploto", width / 2, height / 2);
     text("Presiona T para reiniciar", width / 2, height / 3);
   }

}

  




function keyPressed() {
  let keyValue = key.toUpperCase();
  if(validChars.includes(keyValue)){
    BombTask(keyValue);
 
    
  }

}
function BombTask(keyValue) {
  if (State === "CONFIG") {
    if (keyValue === "A") {
      count = max(10, count + 1);
      } 
    else if (keyValue === "B") {
      count = max(10, count - 1);
    } 
    else if (keyValue === "S") {
      startTime = millis();
      State = "ARMED";
    } 
  }
  else if (State === "ARMED"){
    if (keyValue === "A" || keyValue === "B") {
      llave[keyIndex] = keyValue;
      keyIndex++;
    }
  }
  if (keyIndex === llave.length){
    let passIsOk = true
    for (let i = 0; i < llave.length; i++){
      if(llave[i] !== PASSWORD[i] ){
        passIsOk = false
        break;
      }
    }
    if (passIsOk === true){
      count = 20;
      keyIndex = 0;
      State = "CONFIG";
    }
    else{
      keyIndex = 0;
    }
  }
  else if (State === "EXPLODED") {
    if (keyValue === "T") {
      count = 20;
      startTime = millis();
      State = "CONFIG";
    }
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


