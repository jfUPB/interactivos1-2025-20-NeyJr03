# Unidad 1

## 🤔 Fase: Reflect

### Actividad 07: Autoevaluación

Parte 1: recuperación de conocimiento (Retrieval Practice)

- Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.

   Rta//: Que tiene una interacción entre el software y hardware, tiene una entrada desde un entorno fisico como puede ser un chip, y tiene una retroalimentacion fisica como los leds que componian la mariposa o el corazón

- Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?

   Rta//: Primero el Input	al presionar el botón A del micro:bit, Process que hace la Lectura del dato en p5.js y decisión del color y por ultimo el Output	que es el cambio de color del cuadrado en la pantalla

- ¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?

  Rta//: Esta instrucción envía el carácter 'A' por el puerto del micro:bit cuando se cumple cierta condición (por ejemplo si el botón A está presionado).

- ¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?

   Rta//: La principal diferencia entre el arte/diseño tradicional y el generativo es que el primero depende del control manual del artista, quien toma todas las decisiones y produce una obra única y estática. En cambio, el arte/diseño generativo se basa en sistemas o algoritmos creados por el artista, que permiten a una computadora generar múltiples resultados de manera autónoma o semiautónoma. Así, en el arte generativo, el proceso creativo se comparte entre el ser humano y la máquina.

- Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.

   Rta//: Para que un círculo en p5.js cambie de color al sacudir el micro:bit, se programa el micro:bit para detectar el gesto de “shake” con su acelerómetro y enviar un mensaje (por ejemplo, la letra ‘J’) a través del puerto serial. En p5.js, se usa la biblioteca p5.webserial para escuchar ese mensaje, y cuando se recibe, se ejecuta una función que cambia el color del círculo a uno aleatorio. Así, el movimiento físico del micro:bit se traduce en una acción visual en la pantalla.


Parte 2: reflexión sobre tu proceso (Metacognición)

- ¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?

  Rta//: Siento que una vez entiendo la teoria es más facil para mi ponerlo en práctica y técnica haciendo qu el micro:bit y el p5.js se conecten, por lo que es mas desafiante para mi entender los comandos que se utilizan para que funcione correctamente.

- Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?

   Rta//: Entendi principalmente que por medio de movimientos o interacciones fisicas los botones o el hecho de sacudir el micro:bit se puede programar de muchisimas formas para que respondan a ciertos comandos que deseemos

- Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?

   Rta//: Se volvió un poco mas concreta ya que entiendo las implicaciones que tiene trabajar con estos procesos y el alcance que pueden tener si se usan de cierta manera, entonces el curso adquiere otro significado

- El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?

  Rta//: En lo personal claramente me beneficio seguir un paso a paso, de esta manera estoy seguro de que es lo que estoy haciendo y saber en que parte me pude haber equivado

### Actividad 08: Coevaluación

Aunque ambos logramos que el círculo se moviera horizontalmente usando los botones A y B del micro:bit, pero mi compañero resolvió el problema con alguna cosa diferente a la mía.

Mientras que yo utilicé button_a.is_pressed() y button_b.is_pressed() en el micro:bit para enviar los caracteres 'L' y 'R' continuamente cuando se mantenía presionado el botón, mi compañero optó por button_a.was_pressed() y button_b.was_pressed() para enviar un único mensaje cada vez que se presionaban los botones. Esto hizo que su círculo se moviera en pasos más controlados, uno a uno, con cada clic, en lugar de deslizarse de forma continua como en mi caso.

Aprendí que esa forma de hacerlo puede ser útil si se quiere un control más preciso del movimiento, como en juegos por turnos o interfaces por pasos. Mientras que como yo o hice es mejor cuando se busca una sensación de movimiento más fluida o continuo.


### Actividad 09: Feedback

- Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?

  Rta//: La primera vez que usamos el micro:bit haciendo que se reflejara la mariposa y posteriormente por medio de un codigo cuando se le daba amor se mostraba el corazon por un momento, me hizo entender las posibilidades que tenia con estos procesos


- Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?

  Rta//: En lo personal tuve alguna confusión a la hora de saber donde subir mi bitacora, se me creaban carpetas extra o ponia las cosas donde no, puede que alguna explicacion de todo más a profunidad me hubiera ayudado en su momento


- Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?

  Rta//: Si, me llama mucho la atención que mas posibilidades tiene el trabajar con el microbit, usando otros medios físicos como podria ser la temperatura


- Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?

  Rta//: Me parecio buena la manera de explicar un poco la idea del curso por medio de los videos y luego me parecio organizado el proceso de conectar las herramientas, paso por paso es un buen método


- Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?

  Rta//: Pues me gustó la manera en la que se trabajo, dandonos depronto la posibilidad de llegar a la casa y con calma analizar los procesos


