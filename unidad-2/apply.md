# Unidad 2

## 🛠 Fase: Apply

### Actividad 04: 

<img width="838" height="1022" alt="image" src="https://github.com/user-attachments/assets/7b3d7824-5402-45b2-84b5-1ee188d38b09" />


### Actividad 05:

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
        
        # Armar bomba
        if accelerometer.was_gesture('shake'):
            state = ARMED
            start_time = utime.ticks_ms()
    
    elif state == ARMED:
        elapsed = (utime.ticks_ms() - start_time) // 1000
        remaining = countdown - elapsed

        if remaining >= 0:
            display.show(str(remaining))
        else:
            state = EXPLODED
            display.show(Image.SKULL)
            for _ in range(5):
                beep()
                utime.sleep(0.3)
    
    elif state == EXPLODED:
        if pin_logo.is_touched():
            countdown = 20
            state = CONFIG
            display.show(Image.HAPPY)
