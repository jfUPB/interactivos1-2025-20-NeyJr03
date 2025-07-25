
# Unidad 1

## 🛠 Fase: Apply

### Actividad 05: Interacción básica con micro:bit

Como tal desarrollamos un sistema físico interactivo que conecta una placa micro:bit con un entorno gráfico en p5.js, permitiendo que el comportamiento de un objeto visual (un cuadrado) cambie en tiempo real según las interacciones físicas del usuario (presionar un botón).

Comunicación entre micro:bit y p5.js

- Utilizamos comunicación serial entre el micro:bit y el navegador web usando la librería p5.webserial.js.

- Cuando el botón A del micro:bit se presiona, se envía un carácter 'A' por el puerto serial.

- Cuando no está presionado, se envía un carácter 'N'.

- Este mensaje es leído en p5.js para actualizar el color del cuadrado que se muestra en pantalla.

En cuanto al funcionamiento del código:

- Se inicializa la comunicación serial a 115200 baudios.

- El bucle verifica continuamente si el botón A está presionado.

Resultado:

- El usuario puede interactuar físicamente presionando un botón en el micro:bit.

- Esa acción afecta directamente lo que sucede en la pantalla: el cuadrado se vuelve rojo si se presiona el botón A, o verde si no lo está.

- Este es un ejemplo básico pero poderoso de cómo los mundos físico y digital pueden interactuar en tiempo real usando herramientas accesibles como p5.js y micro:bit.

- Envía 'A' si está presionado y 'N' si no lo está.

- La función sleep(100) hace que se envíen mensajes cada 100ms para mantener actualizada la comunicación.

  

### Actividad 06: Control de movimiento con micro:bit

 Enlace al programa en p5.js:
[https://editor.p5js.org/tu_usuario/sketches/tu_sketch_id](https://editor.p5js.org/JuanJo003/full/4GNdMNvG8)

---

 Código en p5.js

``` js
let port;
let connectBtn;
let x = 200; // Posición inicial del círculo

function setup() {
  createCanvas(400, 400);
  background(220);
  
  port = createSerial();
  connectBtn = createButton('Conectar micro:bit');
  connectBtn.position(10, 10);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.availableBytes() > 0) {
    let data = port.read(1);
    if (data === 'L') {
      x -= 10;
    } else if (data === 'R') {
      x += 10;
    }
  }

  x = constrain(x, 0, width);
  fill('blue');
  ellipse(x, height / 2, 50, 50);

  connectBtn.html(port.opened() ? 'Desconectar' : 'Conectar micro:bit');
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open('MicroPython', 115200);
  } else {
    port.close();
  }
}
```

---

Código del micro:bit

``` py
from microbit import *
uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write('L')
        sleep(300)
    elif button_b.is_pressed():
        uart.write('R')
        sleep(300)
```
