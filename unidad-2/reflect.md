# Unidad 2


## 🤔 Fase: 


### Actividad 06

- Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?:

Rta//: Una máquina de estados es un modelo para usar en computadoras que representa un sistema con un número limitado de estados y transiciones entre ellos. Los cuatro componentes fundamentales que use son: estados, transiciones, eventos y acciones


- Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

Rta//: La técnica de máquina de estados es útil porque permite que el micro:bit esté pendiente de varias cosas al mismo tiempo, como contar el tiempo y detectar si presionamos un botón, sin presentar dificultad. A diferencia de usar sleep(), que "congela" el programa y no deja hacer nada más, con una máquina de estados el programa sigue corriendo todo el tiempo y revisa constantemente en qué estado está y qué debe hacer. Así, todo fluye mejor y se siente más “inteligente”, aunque el micro:bit solo haga una cosa a la vez.


- Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

Rta//: Se que tengo que modificar el estado ARMED pero no se me ocurre como hacer para que se divida a la mitad


- Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

Rta//: Un vector de prueba es como una lista de pasos que usamos para ver si nuestro programa está funcionando bien. Por ejemplo, decimos: “si aprieto este botón cuando la bomba está esperando, debería pasar tal cosa”. Hacemos varias pruebas así para asegurarnos de que todo responda como debería. Es útil porque no tenemos que adivinar si está bien, sino que lo comprobamos paso a paso.


- ¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?

Rta//: Creo que la parte que mas me resulto desafiante fue la actividad 04, porque no tenia muy claro como organizar la informacióny mostrarla


- Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

Rta//: Un error común que encontré fue que al presionar el botón para aumentar el tiempo (UP), el contador subía más de una vez con una sola pulsación. Esto pasaba porque el programa detectaba el botón como presionado durante varios ciclos seguidos. Pensar en términos de estados, eventos y transiciones me ayudó a entender que necesitaba un estado intermedio que esperara a que el botón se soltara antes de volver a permitir el aumento de tiempo. Así, agregué una condición para detectar el cambio de “no presionado” a “presionado”, y eso evitó que el contador subiera varias veces con un solo toque. Pensar en “qué está pasando” (evento), “en qué momento está el programa” (estado) y “qué debe hacer después” (transición), me permitió organizar mejor la lógica y resolver el problema.


- El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

Rta//: Traté primero entenderlo para poder saber que partes iba a implementar primero, sabia que no iba a poder añadir todo a la vez, y conforme algo me funcionaba añadia otra cosa de poco para no dañar nada


- Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

Rta//: Ahora que entiendo el patrón de máquina de estados, creo que podría aplicarlo en un videojuego interactivo, por ejemplo, un juego tipo plataforma donde el personaje cambia de estado: caminando, saltando, atacando o recibiendo daño. Cada una de esas acciones sería un estado diferente, y las teclas que el jugador presiona serían los eventos que hacen que el personaje cambie de estado.



### Actividad 07: 


El diagrama de mi compañero estaba bien estructurado y representaba claramente los diferentes estados de la bomba: configuración, armado, cuenta regresiva y detonación. Sin embargo, le sugerí que podía mejorar la claridad de algunas transiciones agregando etiquetas más descriptivas a los eventos, como “presionar botón A” en lugar de solo “UP”.

En cuanto a su código, me pareció interesante que usó una estructura ligeramente distinta a la mía: él utilizó varias funciones para dividir el código en partes más pequeñas, como una función para actualizar el display y otra para manejar los eventos de los botones. Aunque esto hacía el código más largo, también lo hacía más organizado.

Yo le comenté que en mi caso decidí hacerlo todo dentro del ciclo principal (while True) porque me pareció más fácil de seguir, pero después de ver su enfoque aprendí que separar las funciones puede hacer que el programa sea más fácil de mantener y depurar en el futuro.

También hablamos sobre las pruebas. Él utilizó un conjunto de pruebas para simular los diferentes estados presionando los botones en cierto orden, lo cual me pareció una buena práctica que yo no había considerado tan a fondo.




### Actividad 08: 

- Continuar: ¿Qué actividad, explicación o ejemplo de esta unidad te ayudó más a entender el poder de las máquinas de estados? ¿Qué elemento consideras que es indispensable y debería mantener?

Rta//: La actividad que más me ayudó a entender las máquinas de estados fue cuando diseñamos el diagrama de la bomba. Ver todo organizado por estados y transiciones me hizo entender cómo funciona el sistema paso a paso. Lo que más rescato es hacer ese diagrama antes de programar, porque ayuda a no perderse y a encontrar errores más fácil.

- Dejar de hacer: ¿Hubo algún paso o actividad que te pareció confuso, innecesariamente complicado o que aportó poco a tu aprendizaje? ¿Qué cambiarías o eliminarías?

Rta//: No me parece necesario quitar nada

- Empezar a hacer: ¿Qué te habría ayudado a entender mejor?

Rta//: De manera totalmente personal me habría ayudado ver más ejemplos simples de máquinas de estados aplicadas a cosas cotidianas, como un semáforo o un videojuego. Eso habría hecho más fácil entender la lógica antes de pasar al código.


- Ritmo y dificultad: En una escala del 1 (muy fácil) al 5 (muy difícil), ¿Cómo calificarías la dificultad de pasar del análisis de un programa (Actividad 03) al diseño desde cero de uno complejo (Actividad 04 y 05)? ¿Por qué?

Rta//: 4, Porque siempre hay bastante diferencia, se siente mas guiado las actividades anteriores y ese cambio se nota


- Comentario adicional: ¿Hay algo más que te gustaría compartir sobre tu proceso de aprendizaje en esta unidad? ¿Algún momento de frustración o de “¡Aha!” que quieras destacar?

Rta//: Nada en especifico, solo que e va viendo que esta subiendo la difícultad
