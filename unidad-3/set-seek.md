# Unidad 3

## 🔎 Fase: Set + Seek

## Acitividad 05

### Diagrama

<img width="1981" height="1081" alt="Bomba3 0" src="https://github.com/user-attachments/assets/b9ad4afb-4311-4704-ad35-c0a02ceb699c" />

### Tabla de Vectores

|  | Estado Inicial | Evento Disparador | Acciones | Estado Final |
| --- | --- | --- | --- | --- |
| Vector1 | STATE_INIT | No tiene ningun evento | Inicializamos las variables y mostramos el count = 20 | STATE_CONFIG |
| Vector2 | STATE_CONFIG | event.read() == 'A' | Va a sumarle 1 segundo al contador y mostrarlo en la pantalla | STATE_CONFIG |
| Vector3 | STATE_CONFIG | event.read() == 'B' | Va a restarle 1 segundo al contador y mostrarlo en la pantalla | STATE_CONFIG |
| Vector4 | STATE_CONFIG | event.read() == 'S' | Limpia el evento y comienza la cuenta regresiva | STATE_ARMED |
| Vector5 | STATE_ARMED | utime.ticks_diff(utime.ticks_ms, self.startTime) > 1000 | Va contando el tiempo que configuramos en el estado “STATE_CONFIG” en la pantalla | STATE_ARMED |
| Vector6 | STATE_ARMED | range(len(self.key)): if self.key[i] ≠ self.PASSWORD[i]: | Si la contraseña esta mala, No se reinicia el contador, simplemente se borra lo ingresado y se mantiene en estado “STATE_ARMED” | STATE_ARMED |
| Vector7 | STATE_ARMED | keyindex == len(self.key) && passIsOK | Se reinicia el contador a 20, se reinicia el índice del array y el estado vuelve a “STATE_CONFIG” | STATE_CONFIG |
| Vector8 | STATE_ARMED | count == 0 | Me muestra en la pantalla la imagen de la calavera y viaja a otro estado | STATE_EXPLODED |
| Vector9 | STATE_EXPLODED | event.read() == 'T' | Me muestra el tiempo inicial osea count = 20 | STATE_CONFIG |


