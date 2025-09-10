# Unidad 3


## 🤔 Fase: Reflect


### Refelct Unidad 4

- ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Es como un “idioma común” entre dos dispositivos. Sirve para que ambos entiendan los mensajes y no se confundan.

- ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Porque así es más fácil dividir la información y saber qué dato corresponde a qué cosa.

- ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Para que la computadora sepa cuándo termina un mensaje y no mezcle uno con otro.

- ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
Porque nos ayuda a organizar qué pasa en cada momento (botones, conteo, explosión) sin que el programa se bloquee.

- ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
Se mandan como textos simples, con letras o números, separados por comas o saltos de línea.

- ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
Que cada letra o número se convierte en un código estándar que la computadora puede entender.

- ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
Porque si no hay nada que leer, el programa puede fallar o leer basura.

if (port.availableBytes() > 0) {
    let data = port.readUntil("\n");
}


- ¿Qué hiciste bien en esta unidad que debes continuar haciendo?
Organizar mi código paso a paso y probarlo constantemente.

- ¿Qué deberías comenzar a hacer para mejorar tu proceso?
Planear mejor antes de programar y guardar todo lo que hago para no perderme.
