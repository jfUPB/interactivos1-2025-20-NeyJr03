# Unidad 3


## 🛠 Fase: Apply

###  Actividad 06


```javascript
// --------------------------
// Bomba 2.0 en p5.js
// Máquina de estados aplicada
// --------------------------

let estado = "CONFIG";    // Estados: CONFIG, ARMED, EXPLOSION, DESARMADA
let tiempo = 20;          // Tiempo inicial
let ultimoTiempo = 0;     // Para medir 1 segundo
let secuencia = [];       // Guardar botones presionados (A-B-A)

function setup() {
  createCanvas(400, 200);
  textAlign(CENTER, CENTER);
  textSize(24);
}

function draw() {
  background(30);

  // Mostrar según el estado
  if (estado === "CONFIG") {
    fill(0, 200, 255);
    text("Modo Configuración", width/2, 40);
    text("Tiempo: " + tiempo + "s", width/2, 100);

  } else if (estado === "ARMED") {
    fill(255, 200, 0);
    text("Bomba Armada", width/2, 40);
    text("Tiempo: " + tiempo + "s", width/2, 100);

    // Control del temporizador (1 segundo)
    if (millis() - ultimoTiempo >= 1000) {
      tiempo--;
      ultimoTiempo = millis();
    }

    // Explota si llega a 0
    if (tiempo <= 0) {
      estado = "EXPLOSION";
    }

  } else if (estado === "EXPLOSION") {
    fill(255, 0, 0);
    text("💥 BOOM 💥", width/2, height/2);

  } else if (estado === "DESARMADA") {
    fill(0, 255, 100);
    text("Bomba Desarmada", width/2, height/2);
  }
}

// --------------------------
// Manejo de eventos con teclado
// --------------------------
function keyPressed() {
  if (estado === "CONFIG") {
    if (key === 'A') {      
      if (tiempo < 60) tiempo++;
    }
    if (key === 'B') {      
      if (tiempo > 10) tiempo--;
    }
    if (key === 'S') {      
      // Shake (Armar bomba)
      estado = "ARMED";
      ultimoTiempo = millis();
    }
  }

  // Secuencia para desarmar (A-B-A)
  if (estado === "ARMED") {
    if (key === 'A' || key === 'B') {
      secuencia.push(key);
      if (secuencia.length > 3) secuencia.shift(); // mantener solo 3

      if (secuencia.join('') === "ABA") {
        estado = "DESARMADA";
        secuencia = [];
      }
    }
  }

  // Reset con tecla T (Touch)
  if (key === 'T') {
    estado = "CONFIG";
    tiempo = 20;
    secuencia = [];
  }
}

```




- Logré implementar la bomba 2.0 en p5.js respetando la técnica de máquinas de estado.

- El flujo de estados es: Configuración → Armada → Explosión / Desarmada → Configuración.

- Para simular los sensores del micro:bit usé teclas del teclado:

A → UP

B → DOWN

S → ARMED (shake)

T → TOUCH (reset)

- También programé la secuencia de desarme A-B-A para pasar de armado a desarmada.





### Actividad 07

- Código en p5.js

```javascript
let estado = "CONFIG";
let tiempo = 20;
let ultimoSegundo = 0;

// Serial
let puerto;
let valorSerial = "";

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);

  puerto = new p5.WebSerial();
  puerto.on("data", leerSerial);
  puerto.on("noport", () => puerto.requestPort());
  puerto.open();
}

function draw() {
  background(220);

  if (estado === "CONFIG") {
    text("Tiempo: " + tiempo, width / 2, height / 2);
    text("A=+1  B=-1", width / 2, height / 2 + 40);
    text("A+B = Start", width / 2, height / 2 + 80);
  } else if (estado === "ARMED") {
    text("Tiempo: " + tiempo, width / 2, height / 2);
    if (segundo() !== ultimoSegundo) {
      tiempo--;
      ultimoSegundo = segundo();
    }
    if (tiempo <= 0) {
      estado = "EXPLOTO";
    }
  } else if (estado === "EXPLOTO") {
    text("💥 BOOM 💥", width / 2, height / 2);
  }
}

function leerSerial() {
  let entrada = puerto.readLine().trim();
  if (entrada.length > 0) {
    if (estado === "CONFIG") {
      if (entrada === "A") tiempo++;
      if (entrada === "B") tiempo--;
      if (entrada === "S") estado = "ARMED";
    }
    if (entrada === "T") {
      estado = "CONFIG";
      tiempo = 20;
    }
  }
}
```



- Enlace : [Ver simulación en p5.js](https://editor.p5js.org/JuanJo003/full/akp15rA8n)



- Código en Micro.Bit:

```javascript
input.onButtonPressed(Button.A, function () {
    serial.writeLine("A")
})
input.onButtonPressed(Button.B, function () {
    serial.writeLine("B")
})
input.onButtonPressed(Button.AB, function () {
    serial.writeLine("S")
})
input.onGesture(Gesture.Shake, function () {
    serial.writeLine("T")
})
```





