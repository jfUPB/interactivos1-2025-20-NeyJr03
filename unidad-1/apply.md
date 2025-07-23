
# Unidad 1

## 🛠 Fase: Apply

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
