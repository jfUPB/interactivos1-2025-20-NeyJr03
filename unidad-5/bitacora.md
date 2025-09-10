
# Evidencias de la unidad 5

## Set: 

### Actividad 01 – Caso de estudio
Comunicación entre micro:bit y p5.js

El micro:bit y el sketch de p5.js se comunican mediante el puerto serial (UART).
El micro:bit envía datos continuamente en formato de texto (ASCII) a 115200 baudios, y el navegador los recibe a través de la librería p5.webserial.

Los datos que se envían son:

Valor del acelerómetro en X.

Valor del acelerómetro en Y.

Estado del botón A (1 si está presionado, 0 si no).

Estado del botón B (1 si está presionado, 0 si no).

De esta forma, el micro:bit funciona como un sensor y controlador, y p5.js interpreta esa información para generar los gráficos en la pantalla.

Estructura del protocolo ASCII

El protocolo es muy sencillo:

Cada lectura se empaqueta como una línea de texto con los cuatro valores separados por comas.

Al final se añade un salto de línea \n que marca el fin del mensaje.

Ejemplo de un mensaje real:

```javascript
-23,1045,True,False
```

Esto facilita que en p5.js se pueda separar la cadena en sus cuatro partes usando .split(",").

Lectura de datos en p5.js

En el sketch.js, los datos se leen en la sección:

```javascript
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}
```

Aquí ocurre lo más importante:

Se recibe la línea completa enviada por el micro:bit.

Se divide en cuatro partes.

Los valores de X e Y se transforman en coordenadas de pantalla.

Los estados de los botones se convierten en valores booleanos.

Eventos A pressed y B released

Los eventos no vienen directamente del micro:bit.
El micro:bit solo envía si los botones están en True o False.
En p5.js, la función updateButtonStates() detecta el cambio de estado comparando el valor actual con el anterior:

```javascript

function updateButtonStates(newAState, newBState) {
  if (newAState === true && prevmicroBitAState === false) {
    // Evento: A presionado
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }

  if (newBState === false && prevmicroBitBState === true) {
    // Evento: B liberado
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```

Así es como el código genera eventos a partir de los datos seriales, lo que da la ilusión de que p5.js “sabe” cuándo se presionó o soltó un botón.

Reflexión personal

Este caso de estudio me ayudó a ver cómo una máquina de estados y un protocolo de comunicación sencillo pueden coordinar dos sistemas distintos (micro:bit y navegador).
Al principio pensaba que el micro:bit mandaba directamente “eventos de teclado”, pero en realidad lo que hace es enviar solo números y booleanos. Es p5.js el que interpreta esos cambios y los convierte en eventos útiles para el dibujo.

Me pareció muy interesante que un protocolo tan simple como “valores separados por comas” sea suficiente para sincronizar hardware y software de forma confiable. También entendí mejor por qué es importante el carácter de fin de línea: sin él, los mensajes se mezclarían y sería imposible separar bien cada dato.


### Seek:

Actividad 02 – Caso de estudio: micro:bit (Protocolo Binario)

Código original en ASCII


```javascript
# Imports go at the top
from microbit import *

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
    uart.write(data)
    sleep(100) # Envia datos a 10 Hz

Código modificado con struct.pack
# Imports go at the top
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    uart.write(data)
    sleep(100) # Envia datos a 10 Hz

```

Explicación corta:
El formato >2h2B significa:

>: big-endian (byte más significativo primero).

2h: dos enteros cortos (2 bytes cada uno → 4 bytes en total).

2B: dos enteros sin signo (1 byte cada uno → 2 bytes en total).
Cada mensaje ocupa 6 bytes.

Experimento 1: Datos en modo Texto (SerialTerminal)

Cuando visualicé los datos en modo texto se veía una serie de símbolos extraños. Esto ocurre porque los datos están en formato binario y no corresponden a caracteres ASCII legibles.

Experimento 2: Datos en modo Hexadecimal

En modo Hex pude ver los bytes representados en valores hexadecimales. Esto se relaciona con la línea:

data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))


Cada bloque de 6 bytes representa un mensaje con los valores de aceleración y botones.

Ventajas y desventajas del formato binario

Ventajas:

Ocupa menos espacio (6 bytes en lugar de varias decenas en ASCII).

Se transmite y procesa más rápido.

Desventajas:

No es legible directamente por humanos.

Requiere más cuidado en el manejo del formato para decodificarlo correctamente.

Experimento con detección de movimiento (shake)

Código:


```javascript
# Imports go at the top
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)

```

 Cada mensaje enviado tiene 6 bytes (2+2+1+1). Los primeros 4 corresponden a xValue y yValue (pueden ser positivos o negativos), y los últimos 2 a los botones A y B.

Números negativos en >2h2B

 Los números negativos se representan en complemento a dos dentro de los 2 bytes asignados a cada entero corto. Por eso en Hex aparecen como valores grandes (ej. -1 se ve como FF FF).

Comparación ASCII vs Binario

Código:


```javascript
# Imports go at the top
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0,0,9)

while True:
    if accelerometer.was_gesture('shake'):
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()

        # Envío en binario
        data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
        uart.write(data)

        # Envío en ASCII
        uart.write("ASCII:\n")
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)

```

Diferencias observadas:

Binario → compacto, rápido, eficiente.


### Actividad 04 – Aplicación

Código en Micro:bit


```javascript
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0, 0, 9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    checksum = sum(data) % 256
    packet = b'\xAA' + data + bytes([checksum])
    uart.write(packet)
    sleep(100)

```

- Evidencias:
- Proceso de construcción: 

Empecé con el código de la actividad anterior que enviaba datos binarios.

Agregué un byte de inicio (0xAA) para que el receptor identifique fácilmente cada paquete.

Implementé un checksum con sum(data) % 256 para validar que los datos lleguen completos y sin errores.

Finalmente armé el paquete con b'\xAA' + data + bytes([checksum]) y lo envié por el puerto serial.

- Pruebas intermedias:

Al inicio olvidé importar struct y el código no funcionaba → lo solucioné agregando import struct.

En otra prueba, la aplicación no mostraba nada porque había olvidado sumar el byte de inicio antes del paquete.

Después de corregir esto, pude ver que el receptor recibía los datos de forma clara y con menos errores que antes.

- Errores encontrados y solución:

Bug común: al calcular el checksum usé directamente sum(packet) en lugar de sum(data), lo que daba resultados incorrectos.

Solución: corregí la fórmula para aplicar el checksum solo a los datos (sum(data) % 256).

- Experimentos realizados:

Probé el código en la aplicación SerialTerminal para ver los bytes en hexadecimal.

Se notaba claramente el byte de inicio 0xAA.

El último byte cambiaba de acuerdo al checksum.

Comparé el envío con y sin checksum:

Con checksum → pude detectar si había errores en la transmisión.

Sin checksum → a veces llegaban datos cortados y no era fácil identificarlos.

Moví el micro:bit y presioné botones mientras revisaba los valores.

Vi cómo los bytes del paquete cambiaban según xValue, yValue y el estado de los botones.


- Conclusiones

Entendí que un paquete estructurado (byte de inicio + datos + checksum) es mucho más confiable que enviar solo datos en bruto.

El formato binario es más compacto, aunque menos legible que ASCII, pero es mejor para sistemas donde se necesita velocidad y seguridad.

Aprendí a usar checksum como una forma sencilla de verificar errores en la comunicación serial.

ASCII → legible, fácil de depurar, pero ocupa más espacio y es más lento.



