
# Evidencias de la unidad 5

## Actividad 03

### Preguntas de la Unidad:

**Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.**

Por que al enviar valores en ASCII no tenemos como saber que byte corresponde a cada valor por que estan juntos y toca separarlos o leer los con delimitadores como ( `,` y `n\`) para saber hasta donde llegan los bytes de cada dato y cuando se acaba la linea, en cambio con el nuevo protocolo y enviando los datos en binario, ya estamos delimitando cuandos bytes tiene cada dato, con esta linea `struct.pack('>2h2B')`.

**Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?**

Lo mas evident es que ya no estan las lineas de codigo que me ayudaban a leer por ejemplo el `n\` o el splitter que teniamos antes ahora solo le decimos que llegan 6 bytes, y que me lean 6 bytes y luego segun la posicion de estos bytes se les asigna a las 4 variables que tenemos. Por ejemplo en `microBitX = view.getInt16(0);` lo que entendemos es que al ser un int16 consume 2 espacios de bytes y el (0) se refiere desde donde comienza.

**¿Qué ves en la consola? ¿Por qué crees que se produce este error?**

Lo que se logra ver es que hay un error o un desface en como estan llegando los datos :
Buena linea:`microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false`
Mala linea:`92 microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false`

Y creo que podria ocurrir por que 



### Preguntas de analizis y comprension:


