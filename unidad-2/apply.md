# Unidad 2

## 🛠 Fase: Apply

### Actividad 04: 

<img width="838" height="1022" alt="image" src="https://github.com/user-attachments/assets/7b3d7824-5402-45b2-84b5-1ee188d38b09" />


### Actividad 05:

## Actividad 05:

```python
from microbit import *
import utime

# Estados
CONFIG = 0
ARMED = 1
EXPLODED = 2

# Variables
state = CONFIG
countdown = 20  # tiempo inicial en segundos
start_time = 0

# Inicializar speaker (pin 0)
def beep():
    pin0.write_digital(1)
    utime.sleep_ms(100)
    pin0.write_digital(0)

# Mostrar tiempo en pantalla
def show_countdown(t):
    display.scroll(str(t), wait=False, loop=False)

while True:
    if state == CONFIG:
        display.show(Image.HAPPY)

        # Aumentar tiempo
        if button_a.was_pressed():
            if countdown < 60:
                countdown += 1
                show_countdown(countdown)

        # Disminuir tiempo
        if button_b.was_pressed():
            if countdown > 10:
                countdown -= 1
                show_countdown(countdown)

        # Armar bomba (agitar)
        if accelerometer.was_gesture("shake"):
            state = ARMED
            start_time = utime.ticks_ms()
            display.show(Image.SKULL)

    elif state == ARMED:
        elapsed = utime.ticks_diff(utime.ticks_ms(), start_time)
        remaining = countdown - elapsed // 1000
        show_countdown(remaining)

        if remaining <= 0:
            state = EXPLODED
            beep()
            display.show(Image.SAD)

        # Reiniciar (touch pin 1)
        if pin1.is_touched():
            state = CONFIG
            countdown = 20
            display.clear()

    elif state == EXPLODED:
        # Mantener imagen y permitir reinicio
        if pin1.is_touched():
            state = CONFIG
            countdown = 20
            display.clear()
```

- Vectores de prueba básicos

1. **Aumentar y disminuir tiempo**  
   - Presionar botón A varias veces: el tiempo aumenta hasta 60 s.
   - Presionar botón B varias veces: el tiempo disminuye hasta 10 s.

2. **Armar la bomba**  
   - Agitar el micro:bit para comenzar la cuenta regresiva.

3. **Detonación**  
   - Esperar que el conteo llegue a 0: se activa el speaker y se muestra una cara triste.

4. **Reinicio**  
   - Tocar el pin 1 para reiniciar el sistema a modo configuración.


