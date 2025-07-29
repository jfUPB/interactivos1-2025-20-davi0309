# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01

Describe detalladamente cómo funciona este ejemplo.
Funciona con Update inicializamos unos pixels los cuales inician en un estado "Init" estos pixeles tienen unos parametros al ser creadas y al momento se carga pixel1.updtae() que lo que hace es cargar el metodo de update lo que se pregunta en que estado esta, si esta en init guarda el tiempo actual cambia el estado a "WaitTimeOut" y prende el led, luego se sigue cargando el update pero esta vez como no esta en "init" cambia y va hacia el evento del "WaitTimeOut" que me calcula cuanto tiempo ha pasado desde el "StartTime" y si ha pasado mas que el intervalo, y se carga la accion si esta encendido lo apaga y si esta apagado lo prende y actualiza el "StartTime" y se vuelve a cargar el elif.

¿Cuáles son los estados en el programa?
esperando algo

¿Cuáles son los eventos/inputs en el programa?
si ya icurrio el evento hago otras acciones o las desencadenan

¿Cuáles son las acciones en el programa?
que hago
