
# Evidencias de la unidad 5

## Actividad 01 – Caso de estudio

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

-23,1045,True,False



Esto facilita que en p5.js se pueda separar la cadena en sus cuatro partes usando .split(",").

Lectura de datos en p5.js

En el sketch.js, los datos se leen en la sección:

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


Aquí ocurre lo más importante:

Se recibe la línea completa enviada por el micro:bit.

Se divide en cuatro partes.

Los valores de X e Y se transforman en coordenadas de pantalla.

Los estados de los botones se convierten en valores booleanos.

Eventos A pressed y B released

Los eventos no vienen directamente del micro:bit.
El micro:bit solo envía si los botones están en True o False.
En p5.js, la función updateButtonStates() detecta el cambio de estado comparando el valor actual con el anterior:

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


Así es como el código genera eventos a partir de los datos seriales, lo que da la ilusión de que p5.js “sabe” cuándo se presionó o soltó un botón.

Reflexión personal

Este caso de estudio me ayudó a ver cómo una máquina de estados y un protocolo de comunicación sencillo pueden coordinar dos sistemas distintos (micro:bit y navegador).
Al principio pensaba que el micro:bit mandaba directamente “eventos de teclado”, pero en realidad lo que hace es enviar solo números y booleanos. Es p5.js el que interpreta esos cambios y los convierte en eventos útiles para el dibujo.

Me pareció muy interesante que un protocolo tan simple como “valores separados por comas” sea suficiente para sincronizar hardware y software de forma confiable. También entendí mejor por qué es importante el carácter de fin de línea: sin él, los mensajes se mezclarían y sería imposible separar bien cada dato.

