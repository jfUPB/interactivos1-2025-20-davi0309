# Unidad 4


## 🤔 Fase: Reflect
### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?

De lo que recuerdo son estos protocolos UART que me ayudan a entender como se van a enviar los datos, cuando van a  terminar y los organiza para su comprension en el p5.js, y creo que tambien se definene parametros como la velocidad en la que me llegan los datos.

### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?

por que de otra manera los datos se juntarian los datos y no se podrian leer 

### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
```js
if (port.availableBytes() > 0) {
    let data = port.readUntil("\n");
```
### ¿Qué hiciste bien en esta unidad que debes continuar haciendo?
### ¿Qué deberías comenzar a hacer para mejorar tu proceso?

