# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

Describe detalladamente cómo funciona este ejemplo.
Funciona con Update inicializamos unos pixels los cuales inician en un estado "Init" estos pixeles tienen unos parametros al ser creadas y al momento se carga pixel1.updtae() que lo que hace es cargar el metodo de update lo que se pregunta en que estado esta, si esta en init guarda el tiempo actual cambia el estado a "WaitTimeOut" y prende el led, luego se sigue cargando el update pero esta vez como no esta en "init" cambia y va hacia el evento del "WaitTimeOut" que me calcula cuanto tiempo ha pasado desde el "StartTime" y si ha pasado mas que el intervalo, y se carga la accion si esta encendido lo apaga y si esta apagado lo prende y actualiza el "StartTime" y se vuelve a cargar el elif.

¿Cuáles son los estados en el programa?
son las partes donde se espera algo para poder llevar acabo una accion en este codigo seria el estado `WaitTimeOut` y el pseudo estado `init`.

¿Cuáles son los eventos/inputs en el programa?
Los eventos son los encargados de preguntar si ya ocurrio algo o cambio algo desencadenar una lista de acciones en este caso seria esta linea de codigo:
```javascript
if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
```

¿Cuáles son las acciones en el programa?
que hago

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
