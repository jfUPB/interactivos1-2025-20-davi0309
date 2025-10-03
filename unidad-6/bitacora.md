
# Evidencias de la unidad 6

### **¿Qué ocurrió en la terminal cuando ejecutaste npm install?** 
Me salio en la terminal fue esto:
```
added 120 packages, and audited 121 packages in 4s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice
npm notice New major version of npm available! 10.9.3 -> 11.6.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.6.0
npm notice To update run: npm install -g npm@11.6.0
npm notice

```

### **¿Cuál crees que es su propósito?**

Me imagino que añadio unos paquetes, y informacion general de la descarga, y todo esto para poder cargar el caso de estudio.

### **¿Qué mensaje específico apareció en la terminal después de ejecutar npm start?**

```cpp
> nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000
```

### **¿Qué indica este mensaje?**

Indica que se conecto con el server, y que esta `listening` osea como esperando a que ocurra algo.


### **Describe lo que ves inicialmente en page1 y page2 en tu navegador.**

Lo primero que veo es un especie de cuadrado que dice "sincronizando datos" cuando abro la primera pestaña, cuando abro las dos pestañas se dibujan dos circulos cada uno en una de las pestañas dibujados solo en el centro de la imagen, y tienen una linea que se conecta a cada uno de ellos, por medio de una coneccion. 

### **¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?**

<img width="682" height="315" alt="imagen" src="https://github.com/user-attachments/assets/00136f2f-c53e-461f-adfe-6228c854b11f" />


Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas.

### **¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?**

Lo primero que podemos observar es como en la pestaña no se encuentran aun datos  y aparece `èsperando conexion a otra ventana`, se queda aqui hasta que reciba la señal de cuando se abre la `page2` para poder conectarse

<img width="1919" height="1021" alt="imagen" src="https://github.com/user-attachments/assets/29e43691-910b-49a4-93fc-3f8e2ddd4b3f" />

En esta imagen ya podemos ver como se conectan efectivamente las dos pestañas o paginas generando esta imagen con el cable hacia el centro de el otro, cada pagina le manda al servidor la posicion en la que esta y la ptra la ejecuta y la lee para generar esta linea ya que cada pagina dibuja estos dos circulos.


<img width="1919" height="1011" alt="imagen" src="https://github.com/user-attachments/assets/07809528-448d-4b6e-bcc1-e17e51f23cb4" />


Y esto es lo que me aparece en la consola:


<img width="1502" height="992" alt="imagen" src="https://github.com/user-attachments/assets/98f764e2-d46e-434d-bc82-c389a08f4101" />

# Actividad 02

## **Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.**

En mi casa me conecto a Internet mediante el Wi-Fi, ps todo lo que es mi celular y computador y hasta televisor pero el play si esta conectado por cable LAN, si la rampa se cortara los carros o vehiculos que tengo no podrian ir a la gran acrretera ni poder llegar a ningun lugar que este conectado a esta, qeudandose incomunicados y desconectados de la via (red).

## ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

Cuando se pide un libro en una biblioteca el cliente es el que pide el libro y el servidor es el bibliotecario, la peticion seria pedir el libro y este le devuelbe el libro o los datos de donde esta el libro que busco.

## Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

Por lo que se consulto entendemos que estas URL estan divididas de esta manera: `Protocolo`, `Nombre del dominio` y la `Ruta especifica`.

La pagina que escogi fue Wordle y su URL es: https://www.nytimes.com/games/wordle/index.html

Donde el dominio es: `www.nytimes.com`, el protocolo es: `https://` y la ruta especifica es: `/games/wordle/index.html`.

Si solo escribo el dominio sin una ruta específica, me lleva a otro sitio web.

Me envía por defecto a la página principal del sintio web.

<img width="1919" height="967" alt="imagen" src="https://github.com/user-attachments/assets/c06592a9-c842-4c68-b375-431f6cec42a2" />


<img width="1919" height="959" alt="imagen" src="https://github.com/user-attachments/assets/e0cb8a91-3072-4a73-83c1-6b5515f4b3f1" />

## Compara HTTP con los protocolos seriales que usaste.

**¿Qué similitudes encuentras?**

Se establece un “lenguaje común” con reglas definidas entre quien envía y quien recibe la información: el cliente, como un navegador o un micro:bit, transmite un mensaje y el servidor o receptor responde a esa solicitud.

**¿Qué diferencias clave ves?**

HTTP resulta más complejo porque maneja cabeceras, códigos de estado y tipos de contenido, mientras que Serial es más sencillo ya que únicamente envía bytes sin añadir tanta información extra.

**¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?**

Necesita esta complejidad ya que en HTTP los servidores en la web tienen muchos tipos de datos diferentes como botones, imagenes, texto, videos, etc ... . Además tenemos que aladir que mucha mas gente va a moverse por estas paginas no como lo hemos estado trabajando.

## Piensa en una página web simple, como un formulario de login.

**Piensa en una página web simple, como un formulario de login.**

Vamos a tomar esta pagina principal:

<img width="1919" height="838" alt="imagen" src="https://github.com/user-attachments/assets/00158034-a945-431e-8737-b266751ffdb3" />

**¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?**

HTML: los campos de texto (usuario, contraseña) y el botón y en si es como se ubica todo en la pagina como la estructura o cuerepo por asi decirlo.

**¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?**

CSS: color del botón, tipo de letra, márgenes y estilos visuales, algunas animaciones en los botones y en las letras, tanto como el los logos y demas.

**¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?**

JavaScript: validar que el usuario escribio algo en la barra de la lupa o si presiono algun boton para que lo redireccione a otra pestaña.

## Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.

**¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?**

Es más eficiente porque evita gastar recursos en redibujar constantemente, y resulta más natural para las interfaces, ya que solo responden cuando el usuario interactúa.

**¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?**

Si esto se usa en la web seria demasiado pesado para el rendimiento del programa y pondria muy lento todo ademas de ser ineficiente.

**¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?**

Permite al desarrollador trabajar con un solo lenguaje, reutilizar librerías y lógica —como la validación de formularios en cliente y servidor y lograr así un flujo de desarrollo más ágil y uniforme.

## Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

Ps que en HTTP lo que pasa es que los datos son pedidos y son recibidos con un delay o un tiempo que hace que no se sienta tan inmediato como cuando envias un mensaje con mal internet o cuando te envian un correo en cambio en comunicacion con WebSockets/Socket.IO los datos son instantaneos como si estuvieramos en un stream o una llamada , tambien como un mensaje de whattsapp.

# Actividad 03

## Experimento 1

## Intenta acceder a http://localhost:3000/page1. ¿Funciona?

Si funciona ya que en el codigo esta definido como /page1
<img width="1919" height="755" alt="imagen" src="https://github.com/user-attachments/assets/d5ab28b5-9af7-4561-be54-159abe0530d9" />


## Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona?

Si funciona ya que en el codigo esta definido como /pagina_uno
<img width="1919" height="866" alt="imagen" src="https://github.com/user-attachments/assets/82a97856-8c8b-45f9-8ad7-28d354752ed5" />

¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.

Al cambiar la definición de la ruta en el archivo server.js, el servidor solo responde a esa ruta exacta:
```js
app.get('/pagina_uno', (req, res) => {
```

Esto confirma que el servidor asocia cada URL exactamente con las rutas definidas en el código. Si la ruta no existe, responde con el error Cannot GET.

## Experimento 02

cuando abrimos page1:
<img width="732" height="152" alt="imagen" src="https://github.com/user-attachments/assets/7acd3a9a-fdb3-4ccb-9549-67d3f627fe26" />

cuando abrimos page2:

<img width="729" height="169" alt="imagen" src="https://github.com/user-attachments/assets/b1bde501-b4a8-4280-8f6a-8638113b4c99" />

Al cerrar page1:

<img width="423" height="17" alt="imagen" src="https://github.com/user-attachments/assets/621c0a5d-b13b-416e-a351-b1a7e448105b" />

Al cerrar page2:

<img width="414" height="25" alt="imagen" src="https://github.com/user-attachments/assets/92d54c48-dc76-4114-a79e-7a9bab386e91" />

Cada vez que un cliente se conecta, el servidor le asigna un ID único que varía según la pestaña o dispositivo. Al cerrarse una pestaña, la terminal muestra el mensaje de desconexión con ese mismo ID, lo que permite identificar a cada conexión de manera individual y demuestra cómo Socket.IO maneja varias conexiones al mismo tiempo distinguiendo a los clientes por su identificador.

## Experimento 03

<img width="731" height="387" alt="imagen" src="https://github.com/user-attachments/assets/9ccca4f7-5a6a-4dd8-882f-c0255a4c9f73" />

<img width="727" height="377" alt="imagen" src="https://github.com/user-attachments/assets/3a9e9eeb-62cb-44ba-955f-5a973287ba23" />

Luego de haber modificado el código:

<img width="712" height="384" alt="imagen" src="https://github.com/user-attachments/assets/5a5d9780-ea43-406e-a74b-7d18bec5bae5" />


<img width="1919" height="995" alt="imagen" src="https://github.com/user-attachments/assets/3fdbe888-94cb-4c01-8734-61f636c1f14d" />

Cada cliente que se conecta envía al servidor la información de su ventana (posición y tamaño), y este mantiene un estado compartido que refleja quién está en page1 y quién en page2. En la consola puede verse cómo, al unirse dos clientes, el servidor registra Page1: 1, Page2: 1 y luego muestra All clients are fully synced, señal de que ambos enviaron sus datos y la sincronización terminó. En el navegador, page1 visualiza los dos nodos unidos por una línea, mientras que page2 solo muestra su propio círculo. Esto evidencia que el servidor funciona como intermediario entre los clientes, garantizando un estado común y la coherencia en la comunicación en tiempo real.

## Experimento 04

### Inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando?

<img width="447" height="123" alt="imagen" src="https://github.com/user-attachments/assets/a5033250-72b8-418d-93f1-f4fb2f4b4f8d" />

**Intenta abrir http://localhost:3000/page1. ¿Funciona?**

<img width="955" height="998" alt="imagen" src="https://github.com/user-attachments/assets/dbe66107-5577-4144-a6f2-115edbae2b5d" />

**Intenta abrir http://localhost:3001/page1. ¿Funciona?**

Aqui si funciona ya que si responde a 3001

<img width="947" height="1007" alt="imagen" src="https://github.com/user-attachments/assets/998e0015-4296-4077-86ed-2c095309d658" />

**¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.**

Al modificar la constante port a 3001, el servidor deja de atender en 3000 y pasa a responder únicamente en 3001, lo que muestra que esta variable define el puerto de escucha y que la función server.listen(port) abre la conexión en ese punto específico. Si se intenta conectar a un puerto distinto, no habrá servidor que responda.

# Actividad 05

## Idea

Bueno quiero crear algo llamado como `"fabrica de estrellas"` donde podras en una pagina crear circulos y o puntitos y esta tambien tiene un boton que dice cambiar color, este no va a cambiar nada en la pagina1 pero si en la pagina2 generando colores aleatorios para estas estrellas.

### Evidencia

<img width="1919" height="954" alt="imagen" src="https://github.com/user-attachments/assets/e396caf9-51d1-455d-8e6f-05ece023abf6" />


<img width="1919" height="934" alt="imagen" src="https://github.com/user-attachments/assets/91e25f4f-9ec1-4ce4-b655-8e8bc97d940f" />

### Implementación

La aplicación se construyó usando:

Servidor con Node.js.
Comunicación en tiempo real con Socket.IO.
Interfaz cliente con java.
El usuario (interactivo) y espectador (observador).

### Codigo

`seve.js`

```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };
let connectedClients = new Map();
let syncedClients = new Set();

let stars = [];  // almacena todas las estrellas creadas
let colorPage2 = [255, 255, 0]; // color inicial amarillo en page2

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected - ID:', socket.id);
    connectedClients.set(socket.id, { page: null, synced: false });

    // Enviar estado inicial de estrellas
    socket.emit('initStars', { stars, color: colorPage2 });

    // Recibir nuevas estrellas desde Page1
    socket.on('newStar', (star) => {
        stars.push(star);
        io.emit('newStar', star); // enviar a todos los clientes
    });

    // Cambiar color de estrellas en Page2
    socket.on('changeColor', (newColor) => {
        colorPage2 = newColor;
        io.emit('changeColor', newColor);
    });

    socket.on('disconnect', () => {
        console.log('User disconnected - ID:', socket.id);
        connectedClients.delete(socket.id);
        syncedClients.delete(socket.id);
        socket.broadcast.emit('peerDisconnected');
    });

    // Tu lógica original de win1update y win2update (sin cambios)
    socket.on('win1update', (window1, sendid) => {
        if (isValidWindowData(window1)) {
            page1 = window1;
            connectedClients.set(socket.id, { page: 'page1', synced: false });
            socket.broadcast.emit('getdata', { data: page1, from: 'page1' });
            checkAndNotifySyncStatus();
        }
    });

    socket.on('win2update', (window2, sendid) => {
        if (isValidWindowData(window2)) {
            page2 = window2;
            connectedClients.set(socket.id, { page: 'page2', synced: false });
            socket.broadcast.emit('getdata', { data: page2, from: 'page2' });
            checkAndNotifySyncStatus();
        }
    });

    socket.on('requestSync', () => {
        const clientInfo = connectedClients.get(socket.id);
        if (clientInfo?.page === 'page1') {
            socket.emit('getdata', { data: page2, from: 'page2' });
        } else if (clientInfo?.page === 'page2') {
            socket.emit('getdata', { data: page1, from: 'page1' });
        }
    });

    socket.on('confirmSync', () => {
        syncedClients.add(socket.id);
        const clientInfo = connectedClients.get(socket.id);
        if (clientInfo) {
            connectedClients.set(socket.id, { ...clientInfo, synced: true });
        }
        checkAndNotifySyncStatus();
    });
});

function isValidWindowData(data) {
    return data &&
        typeof data.x === 'number' &&
        typeof data.y === 'number' &&
        typeof data.width === 'number' && data.width > 0 &&
        typeof data.height === 'number' && data.height > 0;
}

function checkAndNotifySyncStatus() {
    const page1Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page1');
    const page2Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page2');

    const bothPagesConnected = page1Clients.length > 0 && page2Clients.length > 0;
    const allClientsSynced = Array.from(connectedClients.keys()).every(id => syncedClients.has(id));
    const hasMinimumClients = connectedClients.size >= 2;

    if (bothPagesConnected && allClientsSynced && hasMinimumClients) {
        io.emit('fullySynced', true);
        console.log('All clients are fully synced');
    } else {
        io.emit('fullySynced', false);
    }
}

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});

```
`Page1.js`
```js
let stars = [];
let socket;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(0);

    socket = io();

    socket.on('initStars', (data) => {
        stars = data.stars || [];
        redrawStars();
    });

    socket.on('newStar', (star) => {
        stars.push(star);
        drawStar(star.x, star.y, color(0, 0, 255)); // azul en Page1
    });

    // Botón para cambiar color en Page2
    let btn = createButton("Cambiar color en Page2");
    btn.position(20, 20);
    btn.mousePressed(() => {
        socket.emit("changeColor", [random(255), random(255), random(255)]);
    });
}

function mousePressed() {
    let star = { x: mouseX, y: mouseY };
    stars.push(star);
    drawStar(mouseX, mouseY, color(0, 0, 255));
    socket.emit('newStar', star);
}

function drawStar(x, y, c) {
    fill(c);
    noStroke();
    ellipse(x, y, 20, 20);
}

function redrawStars() {
    background(0);
    for (let s of stars) {
        drawStar(s.x, s.y, color(0, 0, 255));
    }
}

```
`Page2.js`

```js
let stars = [];
let socket;
let starColor = [255, 255, 0]; // amarillo inicial

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(0);

    socket = io();

    socket.on('initStars', (data) => {
        stars = data.stars || [];
        starColor = data.color || [255, 255, 0];
        redrawStars();
    });

    socket.on('newStar', (star) => {
        stars.push(star);
        drawStar(star.x, star.y, color(...starColor));
    });

    socket.on('changeColor', (newColor) => {
        starColor = newColor;
        redrawStars();
    });
}

function drawStar(x, y, c) {
    fill(c);
    noStroke();
    ellipse(x, y, 20, 20);
}

function redrawStars() {
    background(0);
    for (let s of stars) {
        drawStar(s.x, s.y, color(...starColor));
    }
}

```

### Conclusion

Aqui pude observar como usar lo de observador y usuario, ademas de la tecnologia en tiempo real y una experiencia diferente al ejemplo.

### Auto evaluacion

| Actividad | Calificación | Justificación |
| --- | --- | --- |
| 1.Actividad | 5 / 5.0 | En el proceso dejé registrado cada fase: desde la instalación de **Node.js** y **npm** hasta la configuración inicial que permite que las páginas puedan comunicarse entre sí.
Para respaldar todo el procedimiento, añadí capturas de pantalla que muestran cada uno de los pasos realizados. |
| 2.Actividad | 5 / 5.0 | Realicé la prueba con el caso de estudio inicial, que consistía en la comunicación entre cliente y servidor, durante el proceso observé cómo funcionaba la interacción y dejé constancia de los resultados obtenidos. |
| 3.Actividad | 5 / 5.0 | Anoté los inconvenientes que aparecieron en el desarrollo, como los errores en **server.js** y los conflictos entre ramas en **Git**.
Además, dejé documentado el proceso de solución y las conclusiones alcanzadas tras resolver cada caso. |
| 4.Actividad | 0 / 5.0 | No pude realizar la actividad |
| 5.Actividad | 4.6/ 5.0 | Implementé el sistema cliente/servidor (server.js, garden.js, spectator.js) y confirmé que funcionara bien con varios clientes en tiempo real.
Registré los códigos completos en la bitácora, **pero** no se logró que las figuras parecieran realmente estrellas, los colores pudieron haberse mejorado y en la consola no se muestra claramente dónde se crearon las estrellas. |

Nota final:
3.96 ya que las actividades realizadas se cumplieron pero no se realizo la actividad 04 y eso tiene un peso en la nota






















