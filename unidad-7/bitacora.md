
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

Funciona para que las direcciones queden enviadas hacia la carpeta public y no tener que generar rutas especificas para cada parte de la carpeta, lo que permite que si se piden datos els ervidor se pa donde buscarya que el control es automatico, en cambio si usamos el app.get(‘/ruta’, …), tenemos o toca definir las rutas especificas y colcoa mas codigo por cada cosa que se pida en las carpetas.















