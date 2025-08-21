# Unidad 3


## 🛠 Fase: Apply
Codigo funcional sin PASSWORD.
```js


let validChars = "ABST";


let count = 20;
let PASSWORD = ["A", "B", "C"];
let llave = [" ", " ", " "];
let KeyIndex = 0;
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
}

```
