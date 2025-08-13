# Unidad 2

## 🔎Fase: Set+Seek

### Actividad 1
---
El programa implementa una máquina de estados para controlar el encendido y apagado de dos píxeles en la matriz LED del micro:bit.  
Cada píxel se define como un objeto de la clase `Pixel`, la cual administra su estado, tiempo de cambio y visualización en pantalla.  

El flujo de ejecución para cada píxel es el siguiente:
1. Inicia en el estado **"Init"**, donde registra el tiempo actual (`startTime`) y muestra el píxel con su valor inicial.
2. Cambia al estado **"WaitTimeout"**, donde permanece verificando si el tiempo transcurrido supera el intervalo configurado.
3. Al cumplirse el intervalo, alterna el valor del píxel entre encendido (valor 9) y apagado (valor 0), actualiza el tiempo de referencia y repite el ciclo.

El programa principal ejecuta continuamente el método `update()` de ambos píxeles, provocando que cada uno parpadee de forma independiente:  
- **Pixel 1**: posición `(0,0)`, intervalo de **1000 ms**.  
- **Pixel 2**: posición `(4,4)`, intervalo de **500 ms**.  

---

 **Estados del programa**
- **Init**: Estado inicial; configura el tiempo de referencia y enciende o apaga el píxel según el estado inicial definido.  
- **WaitTimeout**: Estado de espera; mide el tiempo transcurrido y, al cumplirse el intervalo, alterna el estado del píxel y actualiza la visualización.

---

 **Eventos (Inputs)**
- **Inicio del programa**: Creación de los objetos `Pixel` y primera invocación del método `update()`.  
- **Tiempo transcurrido mayor que el intervalo establecido**: Condición que provoca el cambio de estado del píxel.

---

 **Acciones**
- Registrar el tiempo actual (`startTime`).  
- Alternar el valor del píxel entre encendido (`9`) y apagado (`0`).  
- Actualizar la visualización del píxel en la matriz LED (`display.set_pixel()`).


### Actividad 02


---

 **Código en MicroPython**
```python
from microbit import *
import utime

class Semaforo:
    def __init__(self):
        self.state = "Rojo"
        self.startTime = utime.ticks_ms()
        self.intervalos = {
            "Rojo": 3000,      # 3 segundos
            "Verde": 3000,     # 3 segundos
            "Amarillo": 1000   # 1 segundo
        }

    def mostrar_estado(self):
        display.clear()
        if self.state == "Rojo":
            display.set_pixel(2, 0, 9)  # LED superior
        elif self.state == "Verde":
            display.set_pixel(2, 4, 9)  # LED inferior
        elif self.state == "Amarillo":
            display.set_pixel(2, 2, 9)  # LED central

    def update(self):
        # Mostrar el estado actual
        self.mostrar_estado()

        # Verificar si ha pasado el tiempo del estado actual
        if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.intervalos[self.state]:
            self.startTime = utime.ticks_ms()
            if self.state == "Rojo":
                self.state = "Verde"
            elif self.state == "Verde":
                self.state = "Amarillo"
            elif self.state == "Amarillo":
                self.state = "Rojo"

# Crear semáforo
semaforo = Semaforo()

Así quedaría correcto y el texto posterior se verá normal:

```

Estados del programa
Rojo: LED superior encendido.

Verde: LED inferior encendido.

Amarillo: LED central encendido.

Eventos (Inputs)
Tiempo transcurrido mayor que el intervalo del estado actual: provoca la transición al siguiente color del semáforo.

Acciones
Limpiar la pantalla (display.clear()).

Encender el LED correspondiente al estado actual (display.set_pixel()).

Cambiar el valor de self.state al siguiente en la secuencia.

Actualizar el tiempo de referencia (self.startTime).


### Actividad 03

from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3

HAPPY_INTERVAL = 1500
SMILE_INTERVAL = 1000
SAD_INTERVAL = 2000

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY

    elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE

    elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD

    elif current_state == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
            
- Explicación de la concurrencia
Este programa logra realizar dos tareas de forma concurrente:

Secuencia automática de imágenes: Cambia entre feliz → sonriente → triste → feliz siguiendo intervalos de tiempo establecidos.

Respuesta inmediata a la interacción del usuario: Si el botón A es presionado, el ciclo se interrumpe y cambia inmediatamente al estado correspondiente, sin esperar que termine el intervalo.

Esto se logra evaluando en cada iteración del bucle principal tanto el evento de tiempo como el evento de botón, evitando el uso de pausas largas que bloqueen la ejecución.

- Estados del programa
STATE_INIT: Configura la primera imagen (feliz).

STATE_HAPPY: Muestra cara feliz durante 1500 ms o hasta presionar el botón A.

STATE_SMILE: Muestra cara sonriente durante 1000 ms o hasta presionar el botón A.

STATE_SAD: Muestra cara triste durante 2000 ms o hasta presionar el botón A.

- Eventos
Presionar botón A.

Tiempo transcurrido mayor que el intervalo del estado actual.

- Acciones
Mostrar imagen (display.show(...)).

Actualizar tiempo (start_time = utime.ticks_ms()).

Ajustar intervalo (interval = ...).

Cambiar estado (current_state = ...).


- Vectores de prueba

Vector de prueba 1
Condición inicial: Estado = STATE_HAPPY, imagen feliz.

Evento: Tiempo > 1500 ms.

Esperado: Estado → STATE_SMILE, imagen sonriente, intervalo = 1000 ms.

Resultado: (ver ejecución).


Vector de prueba 2
Condición inicial: Estado = STATE_SMILE, imagen sonriente.

Evento: Botón A presionado.

Esperado: Estado → STATE_HAPPY, imagen feliz, intervalo = 1500 ms.

Resultado: (ver ejecución).


Vector de prueba 3
Condición inicial: Estado = STATE_SAD, imagen triste.

Evento: Botón A presionado.

Esperado: Estado → STATE_SMILE, imagen sonriente, intervalo = 1000 ms.

Resultado: (ver ejecución).
