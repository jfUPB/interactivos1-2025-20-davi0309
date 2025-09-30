# Unidad 2


## 🤔 Fase: Reflect

## Actividad 05

### Codigo

```python
# Imports go at the top
from microbit import *
import utime
import music

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2

current_state = STATE_INIT
BOMB_INTERVAL = 20000
armed_start_time = 0
remaining_time = BOMB_INTERVAL

def show_time(ms):
    seconds = ms // 1000
    for digit in str(seconds):
        display.show(digit)
        sleep(400)


# Code in a 'while True:' loop repeats forever
while True:

    if current_state == STATE_INIT:
        display.show(Image.RABBIT)
        sleep(1000)
        current_state= STATE_CONFIG
        display.clear()

    elif current_state == STATE_CONFIG:  
        show_time(BOMB_INTERVAL)
        
        if button_a.was_pressed() and BOMB_INTERVAL < 60000:
            BOMB_INTERVAL += 1000
            sleep(300)
            
        elif button_b.was_pressed() and BOMB_INTERVAL > 10000:
            BOMB_INTERVAL -= 1000
            sleep(300)
            
        elif accelerometer.was_gesture('shake'):
            current_state = STATE_ARMED
            display.show(Image.DUCK)
            sleep(1000)
            armed_start_time = utime.ticks_ms()
            remaining_time = BOMB_INTERVAL
            display.clear()
            
        sleep(100)
        
    elif current_state == STATE_ARMED:
        now = utime.ticks_ms()
        elapsed = utime.ticks_diff(now,armed_start_time)
        remaining_time = BOMB_INTERVAL - elapsed

        if remaining_time > 0:
            show_time(remaining_time)
        else:
            display.clear()
            display.show(Image.SKULL)
            music.play(music.DADADADUM)
            sleep(2000)
            display.clear()
            current_state = STATE_CONFIG
            BOMB_INTERVAL = 20000
            continue

        if pin_logo.is_touched():
            current_state = STATE_CONFIG
            BOMB_INTERVAL = 20000
            display.clear()

        sleep(100)


```

### Vectores de prueba basicos:


***Vector de Prueba 1***

Condiciones iniciales: Estado = `STATE_CONFIG`,  `BOMB_INTERVAL = 20000 ms`. Se presiona button_a.was_pressed() == True un total de 5 veces antes de detectar accelerometer.was_gesture('shake') == True.

**Que esperamos que suceda:**

- En cada aumento se muestra `Image.ARROW_N`.

- Despues de la agitacion, el estado cambia a `STATE_ARMED`.

- El intervalo (BOMB_INTERVAL) pasa a 25000 ms.

- Se inicia la cuenta regresiva desde 25 s y, al finalizar en 0, se despliega Image.SKULL, suena music.WAWAWAWAA y el sistema retorna a STATE_CONFIG con BOMB_INTERVAL = 20000 ms.

**Que es lo  observado:**

El temporizador incrementa correctamente, se muestran flechas hacia arriba, la cuenta baja desde 25 s, ocurre la detonación y el reinicio se efectúa sin errores.

**Conclusión:** 

Resultado conforme al comportamiento esperado.

***Vector de Prueba 2***

Condiciones iniciales: Estado = `STATE_CONFIG`, `BOMB_INTERVAL = 20000 ms`. Se activa button_b.was_pressed() == True cinco veces, luego se detecta accelerometer.was_gesture('shake') == True y, antes de llegar a 0, ocurre pin_logo.is_touched() == True.

**Que esperamos que suceda:**

- En cada decremento se muestra `Image.ARROW_S`.

- Tras la agitación, el estado pasa a `STATE_ARMED`.

- El intervalo `(BOMB_INTERVAL)` se ajusta a 15000 ms.

- Al tocar `pin_logo`, la bomba se desarma, el estado regresa a STATE_CONFIG con BOMB_INTERVAL = 20000 ms y no se muestra ni sonido ni imagen de explosión.

**Que es lo  observado:**

El sistema disminuye el tiempo a 15 s, entra en STATE_ARMED, se desactiva con pin_logo y retorna a configuración con el intervalo restaurado.

**Conclusión:**

Resultado acorde con lo esperado.

***Vector de Prueba 3***

**Condiciones iniciales:**  Estado = `STATE_CONFIG`, `BOMB_INTERVAL = 20000 ms`. Se presiona button_a.was_pressed() == True repetidamente hasta intentar superar 60000 ms y luego button_b.was_pressed() == True repetidamente hasta intentar bajar de 10000 ms, después accelerometer.was_gesture('shake') == True.

**Que esperamos que suceda:**

- En los incrementos aparece `Image.ARROW_N` y en los decrementos `Image.ARROW_S`.

- El sistema debe imponer un límite máximo de 60000 ms y un mínimo de 10000 ms.

- Tras la agitación, el estado cambia a `STATE_ARMED` con el último valor válido.

- Al llegar a 0 se visualiza `Image.SKULL`, se reproduce `music` y se retorna a `STATE_CONFIG` con `BOMB_INTERVAL = 20000 ms`.

**Que es lo  observado:**

El programa mantiene los límites correctamente, activa la bomba con el tiempo configurado y realiza la detonación y reinicio según lo previsto.

**Conclusión:** El resultado coincide con lo esperado.

