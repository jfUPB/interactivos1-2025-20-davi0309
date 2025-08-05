# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

Describe detalladamente cómo funciona este ejemplo.

Funciona con Update inicializamos unos pixels los cuales inician en un estado "Init" estos pixeles tienen unos parametros al ser creadas y al momento se carga pixel1.updtae() que lo que hace es cargar el metodo de update lo que se pregunta en que estado esta, si esta en init guarda el tiempo actual cambia el estado a "WaitTimeOut" y prende el led, luego se sigue cargando el update pero esta vez como no esta en "init" cambia y va hacia el evento del "WaitTimeOut" que me calcula cuanto tiempo ha pasado desde el "StartTime" y si ha pasado mas que el intervalo, y se carga la accion si esta encendido lo apaga y si esta apagado lo prende y actualiza el "StartTime" y se vuelve a cargar el elif.

¿Cuáles son los estados en el programa?

Son las partes donde se espera algo para poder llevar acabo una accion en este codigo seria el estado `WaitTimeOut` y el pseudo estado `init`.

¿Cuáles son los eventos/inputs en el programa?

Los eventos son los encargados de preguntar si ya ocurrio algo o cambio algo desencadenar una lista de acciones en este caso seria esta linea de codigo:
```javascript
if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
```

¿Cuáles son las acciones en el programa?

Las acciones representan que hace el programa al entrar a un evento en el caso de este software las acciones serian las de prender los pixeles y de contar el tiempo en el que el pixel tiene que estar prendido y apagado.

### Actividad 02

```javascript
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Quieto"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState
        self.next = None

    def set_next(self, next_pixel):
        self.next = next_pixel
           
    def activar(self):
        if self.state == "Quieto":
            self.state = "Espera"

    def update(self):
        if self.state == "Espera":
            self.pixelState = 9
            self.startTime = utime.ticks_ms()
            self.state = "Activo"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "Activo":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.pixelState = 0
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)
                self.state="Quieto"
                if self.next:
                    self.next.activar()

pixel1 = Pixel(2,0,0,5000)
pixel2 = Pixel(2,1,0,2500)
pixel3 = Pixel(2,2,0,10000)

pixel1.set_next(pixel2)
pixel2.set_next(pixel3)
pixel3.set_next(pixel1)

pixel1.activar()

while True:
    pixel1.update()
    pixel2.update()
    pixel3.update()
```

Identifica los estados, eventos y acciones en tu código.

- Estados: 
  - `"QUIETO"` que es el subestado (init) en los codigos anteriores.
  - `"ESPERA"` es el encargado de se activar el píxel, encenderlo, y hacer que empieze a contar el tiempo.
  - `"ACTIVO"` significa que el pixel esta prendido y espera a que pase el tiempo del interval.
- Eventos:
  - los eventos de este software son muy parecidos a los de la Actividad 01 ya que es el paso del tiempo: en esta linea de codigo
  - ```javascript
    utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.interval
    ```
    Aqui se evalúa en estado "Activo". Si se cumple, significa que el tiempo ya pasó, y el píxel debe apagarse y activar al siguiente.
- Acciones:
  - Prende el pixel.
  - Guarda el tiempo de inicio.
  - Cambia a estado activo.
  - Apaga el pixel.
  - cambia a estado `"QUIETO"`.
  - y activa el siguiente pixel.

### Actividad 03
1.Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.

Por que mientras espero que pase el tiempo que debe estar la cara encendida o apagada puedo seguir usando más acciones de manera concurrente en el primer momento  espero el teimpo y puedo colocar la cara feliz para hacer varias acciones en el mismo tiempo, asi se pueden hacer multiples tareas.

2.Identifica los estados, eventos y acciones en el programa.
- Estados:
  - STATE_INIT
  - STATE_HAPPY
  - STATE_SMILE
  - STATE_SAD

- Eventos:
  
Las condiciones de espera del programa son si ya paso un segundo y medio con la cara feliz, espero a que pase 1 segundo en smile y espero a que pase 2 segundos en triste, y si el boton A esta siendo presionado.

- Acciónes:
  - Mostrar la imagen correspondiente al estado actual.
  - Reiniciar el contador de tiempo `start_time`).
  - Asignar un nuevo intervalo.

3.Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.

- Vector de prueba 01
  
Vamos a verificar la transicion de `STATE_INIT` a `STATE_HAPPY` y la condicion con la que inicia es el estado `STATE_INIT`, y no hay eventos externos asi que el programa no genera otro evento, los resultados que se esperan son que se muestre la imagen de happy, guarda el tiempo `start_time`, y transiciona al estado `STATE_HAPPY`.
```javascript
if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY
```
y se llega al resultado esperado.

- Vector de prueba 02
  
Vamos a verificar la transicion de `STATE_HAPPY` a `STATE_SAD` cuando se presiona el boton A, y la condicion con la que inicia es el estado `STATE_HAPPY`, el evento que se espera es que se presione el boton A y se devuelve un true, los resultados que se esperan son que se muestre la imagen de sad, se actualize el tiempo para que comience otra vez y no allan problemas con los intervalos de estos en `start_time`, y transiciona al estado `STATE_SAD`.
```javascript
elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            # Acciones para el evento
            display.show(Image.SAD)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
```
Y carga como se esperaba.

- Vector de prueba 03
  
Vamos a verificar la transicion por tiempo de `STATE_SAD` a `STATE_SMILE`, y la condicion con la que inicia es el estado `STATE_SAD`, `start_time = t0` y el tiempo acyual `t > t0 + interval`, el evento que se espera es que es la evaluacion de `utime.ticks_diff(utime.ticks_ms(), start_time) > interval` que se cumple en este caso, los resultados que se esperan son que se muestre la imagen de smile, se actualize el tiempo para que comience otra vez y se establezca el intervalo de del estado smile, y transiciona al estado `STATE_SMILE`.
```javascript
current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            # Acciones para el evento
            display.show(Image.SMILE)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
```
y se logro lo que se esperaba de esta parte del programa.



