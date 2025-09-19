
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

Lo que pasa es que cuando el SerialTerminal se configura para mostrar `Texto`, los datos binarios que recibe se interpretan como si fueran caracteres ASCII pero es que estos datos no fueron generados para ser leídos como texto ya que el programa intenta convertir secuencias de 0s y 1s en letras o ps algo que podamos leer pero al no tener una referencia clara en la tabla ASCII para esas combinaciones de bits, el resultado son caracteres de pregunta, osea que no lo puede transformar o traducir.

¿Cómo se verían esos números en el formato `>2h2B`?

Se ve uan relacion porque en modo Hex, cada byte se muestra como un valor entre 00 y 7F. Esto corresponde exactamente al resultado de empaquetar los valores en binario osea la linea que tenemos de `data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))` que tambien define el orden y tamaño de cada valor. Lo que se ve en Hex como lo que la computadora entiende.

<img width="927" height="628" alt="imagen" src="https://github.com/user-attachments/assets/d1504896-0ed5-4061-80c1-8bc1faf30b00" />


¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?

Las ventajas que tiene el binario serian que ps los programas no tendran que traducir lo que se len envia o lo que les llega ya que procesan directamente en binarios y ps el microbit tambien, y tambien tiene mayor rendimiento cuando enviamos muchos datos, las desventajas seria que es muy dificil de leer para los humanos, y ps que se necesita saber como se van a traducir los datos como unos tipos de pasos de como llegara la informacion para procesarla y traducirla.

**Ahora cambiamos el codigo existemte por este**
```py
# Imports go at the top
from microbit import *
import struct
uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)
```


<img width="1271" height="403" alt="imagen" src="https://github.com/user-attachments/assets/697ce6d0-fc79-4def-a4de-b289c3ff42d7" />



¿Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes que se envían?

En total se estan enviando 2 tipos de datos 2 int t 2 bool por lo que consultando en internet los enteros valen 2 bytes y los booleanos 1 byte por lo tanto por paquete se envian 6 bytes en total, y se envian de esta manera:
- XValue: 2 bytes que es un entero
- YValue: 2 bytes que es un entero
- aState: 1 byte es un booleano
- bState: 1 byte es un booleano

¿Cómo se verían esos números en el formato '>2h2B'?

Los enteros de 16 bits (h) usan complemento a dos.
Ejemplo: -1 se vería como FF FF en Hex.
Ejemplo: -200 se vería como FF 38.
Esto significa que el formato conserva el signo, y tanto números positivos como negativos se pueden representar correctamente.


<img width="1267" height="514" alt="imagen" src="https://github.com/user-attachments/assets/fd70e752-3796-43d7-87e8-da941b914a01" />


**Ahora cambiamos el codigo existemte por este**
```py
# Imports go at the top
from microbit import *
import struct
uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)
        uart.write("ASCII:\n")
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)
```



<img width="1252" height="519" alt="imagen" src="https://github.com/user-attachments/assets/7df6294b-be63-4672-868f-a9999ee922b1" />

¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII? ¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?

Como vemos en las imagenes en ASCII se ve algo asi (-45,1023,1,0) y en binario algo asi (FF D3 03 FF 01 00) por que es en hex, las ventajas de ASCII es que podemos leerlo de manera facil, las desventajas son que es mas lento y pesado, las ventajas del binario es que es ams compacto y facil de entender para la maquina osea consume menos recursos, las desventajas es que necesita un protocolo para entenderse y es ilegible para humanos.








