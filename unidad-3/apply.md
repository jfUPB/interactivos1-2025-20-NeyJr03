# Unidad 3


## 🛠 Fase: Apply

###  Actividad 06

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

    // Control del temporizador
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
    if (key === 'S


- Logré implementar la bomba 2.0 en p5.js respetando la técnica de máquinas de estado.

- El flujo de estados es: Configuración → Armada → Explosión / Desarmada → Configuración.

- Para simular los sensores del micro:bit usé teclas del teclado:

A → UP

B → DOWN

S → ARMED (shake)

T → TOUCH (reset)

- También programé la secuencia de desarme A-B-A para pasar de armado a desarmada.


