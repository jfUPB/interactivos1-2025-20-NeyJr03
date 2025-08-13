# Unidad 2

## 🔎Fase Set+Seek

### Actividad 1

**Análisis de un programa con una máquina de estados simple**

---

 **Descripción del funcionamiento**
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

## **Estados del programa**
- **Init**: Estado inicial; configura el tiempo de referencia y enciende o apaga el píxel según el estado inicial definido.  
- **WaitTimeout**: Estado de espera; mide el tiempo transcurrido y, al cumplirse el intervalo, alterna el estado del píxel y actualiza la visualización.

---

## **Eventos (Inputs)**
- **Inicio del programa**: Creación de los objetos `Pixel` y primera invocación del método `update()`.  
- **Tiempo transcurrido mayor que el intervalo establecido**: Condición que provoca el cambio de estado del píxel.

---

## **Acciones**
- Registrar el tiempo actual (`startTime`).  
- Alternar el valor del píxel entre encendido (`9`) y apagado (`0`).  
- Actualizar la visualización del píxel en la matriz LED (`display.set_pixel()`).


## Actividad 02

# **Bitácora – Actividad 02**
**Implementando un semáforo con máquina de estados**

---
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

## **Código en MicroPython**

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

# Bucle principal
while True:
    semaforo.update()





