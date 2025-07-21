# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01
¿Qué es un sistema físico interactivo?

Es en si un conjunto de componentes físicos como: los componentes de entrada (inputs), los cuales podrían ser: sensores de movimiento, sonido, presión, luz o temperatura, el procesamiento que se hace en un microcontrolador o computadora y son los encargados se analizar y entender los datos de entrada, y los de salida : los cuales son los responsables de generar una respuesta digital o física, en luces, sonidos, movimientos o vibración, estos sistemas reaccionan a tus acciones, combinando software y hardware para interactuar con el usuario de una forma mas dinámica.

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
Como Game Designer y Desarrollador de niveles, podría aplicar los sistemas físicos interactivos al diseño de exhibiciones interactivas o en las muestras de los juegos que se vayan a presentar, especialmente en espacios culturales, educativos o recreativos. Se podría llegar a utilizar sensores de movimiento, pantallas que reconozcan a las e interactúen con las personas y mecanismos de respuesta en tiempo real, sería posible crear experiencias donde el público no solo observe, sino que participe activamente, así se logra una conexión más directa con el usuario y el videojuego que se está enseñando, al hacer que el usuario interactúe de una manera distinta con la interfaz y el juego se logra que sea más memorable el contenido que se presente.

### Actividad 02
¿Qué es el diseño/arte generativo?

El arte generativo es más expresivo y se conecta con lo que siente el artista y lo que quiere transmitir, pero de todas maneras usando Código o herramientas digitales como parte del proceso creativo, en cambio el diseño generativo esta en función de un propósito u objetivo específico, y no se entregan imágenes estáticas si no lo que entregan es un software y utiliza algoritmos para generar más opciones de diseño basadas en reglas, optimizando el proceso de diseño.

¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

Como Game Designer y Desarrollador de niveles podría implementar el arte generativo creando un algoritmo que permita generar mapas, niveles o entornos automáticamente, se podrían generar texturas o niveles que cambien según las decisiones del jugador, para reducir la carga en diseño manual y poder dar re jugabilidad a los jugadores, estos juegos se diferenciarían estéticamente ya que tiene menor recursos gráficos estáticos.

### Actividad 03

Inputs de entrada:
Botón A, Botón B, Sacudir el micro.bit, el Botón de "Send Love" en el p5.js.

Proceso:
El micro.bit detecta los botones o el movimiento y envía datos al computador y el programa recibe los datos que le dimos mediante los inputs y actualiza lo que se ve en la pantalla del computador, si apretamos en "Send love" se le envia una orden o accion al micro.bit para mostrar las imagenes en los leds del micro.bit.

Outputs de salida:
En el computador cambia de color el circulo segun los datos enviados previamente, en el micro.bit se muestran imagenes en los leds de su pantalla uno al iniciar y otro al recibir "h" o "Send Love".

### Actividad 04

[P5-enlace](https://editor.p5js.org/davi0309/sketches/IY58J5_Cs)

codigo de programa de imagenes
`
function setup() {
  createCanvas(600, 400);
  noStroke(); 
  background(random(180,255),random(180,255),random(180,255));
}

function draw() {
  
  var x = random(width);
  var y = random(height);

  var size = random(10, 80);
  
  
  var r = random(120,255);
  var g = random(120,255);
  var b = random(150,255);
  var a = random(80, 225);

  
  let shapeType = int(random(3));

  if (shapeType === 0) {
    
    fill(r, g, b, a);
    ellipse(x, y, size, size);

    
  } else if (shapeType === 1) {
    
    fill(r, g, b, a);
    rect(x, y, size, size);
    
  } 
    
    else if (shapeType === 2) {
    stroke(r, g, b, a);
    strokeWeight(random(0,20));
    let x2 = x + random(-80,80)
    let y2 = y + random(-80,80)
    line(x, y, x2, y2);
    noStroke(); 
  }

  if (frameCount > random(200,500)) {
    noLoop();
  }
}
`
