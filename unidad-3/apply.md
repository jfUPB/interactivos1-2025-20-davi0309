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

