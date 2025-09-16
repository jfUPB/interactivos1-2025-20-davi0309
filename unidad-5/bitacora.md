
# Evidencias de la unidad 5

## Actividad 01

**Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?**

El micro.bit se conecta desde el puerto serial al computador luego escribimos en el p5 el `port = createSerial();` y luego lo abrimos y esto genera que el micro.bit pueda enviarle datos al p5 y tener en cuenta que es en formato ASCII lo que luego sera procesado por p5 para realizar el arte.

**¿Cómo es la estructura del protocolo ASCII usado?**

la estructura creo que es como el orden en que se tienen que recibir los datos y como se envian entonces seria algo asi: (X),(Y),(microBitAState),(microBitBState)\n
Asi como lo tenemos en el codigo se va a splitear por las (,) comas, y termina de leer esa linea cuando encuentra (\n), ya luego cada dato se le por separado y se realiza o se guarda en un espacio de un arreglo distinto.

**Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.**

```js
 microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
```

En esta parte del codigo se reciben los datos del micro.bit y se combierten por ehemplo el microbitX y el microbitY a posiciones en pantalla, y los otros dos a valores booleanos.

```js
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) 
```
Aqui es donde sucede la magia y lee la linea hasta llegar a \n y divide la linea en cuatro valores (de esto se encarga let values = data.split(",");) y luego si son 4 valores los asigna como lo explicamos arriba.
**¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?**

**Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.**


<img width="1362" height="1204" alt="20250912_113432" src="https://github.com/user-attachments/assets/fdad1216-9c75-48f9-ad08-5b0ecfa02cae" />

## Dudas o preguntas que se me generaron o surgieron en el proceso:

### **¿cual es la funcionalidad de push() y pop() en el programa que estamos manejando?**

Lo que hace `push()` es que me guarda el estado actual de la rotacion, las cordenadas, los colores y los estilos de pencil. `pop()` por otra parte restaura ese estado al ultimo que guardo `push()`, osea que al terminar de dibujar osea dejar de presionar la tecla A vuelve al estado de rotacion y coordenadas original, pero ¿que pasaria si no tenemos el push() y el pop()?, pues lo que pasaria es que todo lo que dibujara despues quedaria rotado y afectaria mi dibujo en pantalla.

### **¿Qué pasaría si los datos no llegaran en el orden correcto?**
Si se truecan los valores de X y Y el dibujo saldria distorsionado y no cumpliria con lo que el usuario le esta entregando, si son todos los datos directamente creeria que no se dibujaria por que no se actualizaria correctamente ya que el programa me esta esperando los datos en un orden antes propuesto.

### **¿Qué ventajas ofrece usar un protocolo de envío de 4 valores separados por comas en lugar de mandar cada valor en mensajes independientes?**

La ventaja seria que mi p5.js esta leyendo solo un mensaje por asi decirlo, que los 4 datos se estan recibiendo en un solo mensaje y esto me ayuda a que no se lleguen a perder datos o lleguen de manera desincronizada.

### Experimentación
Que pasaria si enviamos los datos en un orden diferente sera que `data = "{},{},{},{}\n".format(aState, yValue, xValue,bState) ` para saber si otro sensor puede sustituir la funcion por ejemplo del boton `a` o solo no  se dibujan los valores ya que no entran por el tipo de variable entre botones y sensores.
Resuktado:
Efectivamente el programa no dibuja ya que el sensor X no puede sustituir la funcionalidad del boton A, soguen enviandoce cuatro datos pero al no estar en el orden no hacen nada.

### Analisis y reflexion

Al inicio P5 espero un evento, luego la conexion se hace mediante el puerto serial y le damos una velocidad fija de entrada, y se limpia ps como lo que se estaba enviando antes, muy importantye si no queremos que se dibuje basura. Luego llegan una cadena de bytes que se transforman a texto y se parten en 4 valores, ya luego es interpretado por posicion en X, posicion en Y, boton A y boton B. Y la interaccion que tiene el usuario es mover el microbit para dibujar presionar A para dibujar y soltar B para cambiar de color.


## Actividad 02
Evidencia:
<img width="1249" height="391" alt="imagen" src="https://github.com/user-attachments/assets/51455107-ccff-43b2-9cd8-ae8c4e9a48d8" />

¿Por qué se ve este resultado?



<img width="1271" height="403" alt="imagen" src="https://github.com/user-attachments/assets/697ce6d0-fc79-4def-a4de-b289c3ff42d7" />


<img width="1267" height="514" alt="imagen" src="https://github.com/user-attachments/assets/fd70e752-3796-43d7-87e8-da941b914a01" />

<img width="1252" height="519" alt="imagen" src="https://github.com/user-attachments/assets/7df6294b-be63-4672-868f-a9999ee922b1" />








