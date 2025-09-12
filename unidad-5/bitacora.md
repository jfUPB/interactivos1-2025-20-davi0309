
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

**¿cual es la funcionalidad de push() y pop() en el programa que estamos manejando?**





