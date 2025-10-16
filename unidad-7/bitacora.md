
# Evidencias de la unidad 7

## Actividad 01

## Preguntas de entendimiento 

**¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?**

Esta es la URL que obtube https://pqfmh7rt-3000.use2.devtunnels.ms/, creo que necesitamos la otra URL por que como el nombre lo dice es local y por ende no se puede conectar a desde un celular que es completamente aparte ya que local es netamente interno, y la URL especifica es para identificarnos de los otros usuarios.

**Describe brevemente qué hace npm install y npm start**

Npm install, actualiza o descarga todas las dependencias que necesita mi proyecto y npm start, lo pone a correr y carga el servidor.

**¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?****

<img width="599" height="260" alt="imagen" src="https://github.com/user-attachments/assets/d6dd2d8d-60ab-4d7c-9c4c-9ea9a5cb3daa" />

No es diferente ya que manejan ek mismo servidor.

**Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?**

Esta aplicacion esta muy chevere ya que desde el cel puedo mover la pelota, lo que pasa es que si tiene un poco de delay en como se recibe los datos, y si funciono correctamente la interaccion.
Aqui se puede observar como se reciben los datos:

<img width="620" height="411" alt="imagen" src="https://github.com/user-attachments/assets/60a34c9c-dbbd-4b5e-b1bd-143b54a6a28c" />

## Actividad 02

**Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?**

Es un intermediario que sirve como puente para las conecciones en internet, se maneja de manera mucho mas segura y las respuestas del servidor tambien se conectan directamente con los clientes que se conecten deirectamente con la URL de Dev Tunnels, y este reenvía esa conexion de manera segura hacia el servidor local de Node.js

**Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.**

TouchMoved() es una función que se ejecuta automáticamente en un dispositivo con pantalla táctil cada vez que el usuario mueve un dedo en la pantalla sin levantarlo ya que tambien existe touchStarted(), touchEnded() por lo que este tipo de Touch me sirve solo cuando se esta presionando constantemente la pantalla sin levantarlo. Es equivalente a mouseDragged() en un computador con ratón, pero adaptado para pantallas táctiles.
y el threshold es una variable usada para limitar o filtrar la sensibilidad del movimiento, especialmente en celulares no tanto en mouse, ya que depronto el dedo tiembla o se generan movimientos involuntarios que no queremos cargar.


**Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?**

las ventajas de Dev Tunnels son:
> - sirve para conecciones en la msima red local.
> - se puede conectar remotamente aunque no esten en la misma red.
> - se genera un HTTPS automatico.
> - aunque esten los clientes en distintas redes se mantiene la compatibilidad y el flujo.

las desventajas de Dev Tunnels son:
> - Requiere una herramienta como visual code.

las ventajas de IP local son:
> - Funciona para conectarse ne la misma red local.
> - No necesita de una app externa.


las desventajas de IP local son:
> - No se puede conectar, si estan afuera de la red.
> - toca crear el HTTPS.
> - No tiene estabilidad en distintas redes.



**Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).**

Desde mi pc:
<img width="1919" height="916" alt="imagen" src="https://github.com/user-attachments/assets/75c8825d-cfd2-40a1-8d52-ec48115c5236" />

Desde el cel:
![Sin título](https://github.com/user-attachments/assets/847fe341-c86c-45d0-9f50-1c1f00766242)

Si lo muevo es asi el resultado:

<img width="1919" height="971" alt="imagen" src="https://github.com/user-attachments/assets/538e41ee-946a-417f-a619-a29c7460e7d6" />


## Actividad 03

**¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?**

Funciona para que las direcciones queden enviadas hacia la carpeta public y no tener que generar rutas especificas para cada parte de la carpeta, lo que permite que si se piden datos el servidor sepa donde buscarla ya que el control es automatico, en cambio si usamos el app.get(‘/ruta’, …), tenemos o toca definir las rutas especificas y colocar mas codigo por cada cosa que se pida en las carpetas. En la unidad anterior cada página hacía la solicitud de las bibliotecas necesarias que estaban ubicadas en la carpeta public.

**Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?**

Ps la funcion que se encarga de enviar desde ek movil es esta funcion que se encuentra en `/public/mobile`: 
```cpp
function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let touchData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', touchData);

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false;
}
```
esta funcion es la encargada de enviar la informacion si el usuario toca la pantalla con el dedo o con el mouse, y en el primer if que est este `if (socket && socket.connected)` se verifica si hay una conexion activa, si la hay se corre eso si no, no pasa nada, luego calcula la posicion y la envia por medio de `socket.emit('message', touchData);`.

El evento que recibe del servidor es aqui:

```cpp
socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });
```
y lo que hace es recibir el mensaje, luego lo muestra en la consola y por ultimo con `socket.broadcast.emit('message', message);` reenvia este mensaje a todos los clientes conectados.

**Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?**

Como vimos anterior mente el mensaje se envia a todos los clientes conectados, y ambos se actualizan.

**¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?**

El servidor muestra en la consola cuatro tipos de mensajes diferentes: uno indica el puerto de conexión, y los otros tres son respuestas a las acciones de los clientes.
Cuando un cliente se conecta o se desconecta, el servidor lo notifica con un mensaje específico, pero el registro que más aparece es el "Received message =>".
Los mensajes en la consola tienen este formato:

```cpp
Server is listening on http://localhost:3000
New client connected
Received message => { type: 'touch', x: 129, y: 213 }
Client disconnected
```

El mensaje "Received message =>" incluye las coordenadas del toque que realiza el usuario, las cuales se utilizan para que la ruta /desktop actualice la posición del círculo que aparece en pantalla.

## Actividad 04

Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.



















