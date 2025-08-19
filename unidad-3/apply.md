# Unidad 3


## 🛠 Fase: Apply

let port;
let connectBtn;
let count = 20;
let buttonA, buttonB, buttonT, buttonS
let PASSWORD = [" "," "," "]
let keyIndex = 0
function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    
    buttonA = createButton('A');
    buttonA.position(100, 260);
  
    buttonB = createButton('B');
    buttonB.position(150, 260);
  
    buttonT = createButton('T');
    buttonT.position(200, 260);
  
    buttonS = createButton('S');
    buttonS.position(250, 260);
    
    
    
}
function Init(){
  
  state = "CONFIG"
  
}

function draw() {

  textAlign(CENTER);
  text(count, width / 2, height / 2);
  

}
