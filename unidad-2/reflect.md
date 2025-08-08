# Unidad 2


## 🤔 Fase: 


### Actividad 06

-Describe con tus palabras qué es una máquina de estados. ¿Cuáles son sus cuatro componentes fundamentales que has utilizado en esta unidad?:

Rta//: Una máquina de estados es un modelo para usar en computadoras que representa un sistema con un número limitado de estados y transiciones entre ellos. Los cuatro componentes fundamentales que use son: estados, transiciones, eventos y acciones


-Explica por qué la técnica de máquina de estados es tan útil para gestionar la “concurrencia” (atender un temporizador y botones “al mismo tiempo”) en un dispositivo con un solo hilo de ejecución como el micro:bit. ¿Qué problema soluciona en comparación con usar funciones como sleep()?

Rta//: La técnica de máquina de estados es útil porque permite que el micro:bit esté pendiente de varias cosas al mismo tiempo, como contar el tiempo y detectar si presionamos un botón, sin presentar dificultad. A diferencia de usar sleep(), que "congela" el programa y no deja hacer nada más, con una máquina de estados el programa sigue corriendo todo el tiempo y revisa constantemente en qué estado está y qué debe hacer. Así, todo fluye mejor y se siente más “inteligente”, aunque el micro:bit solo haga una cosa a la vez.


-Imagina que tienes que añadir una nueva funcionalidad a la bomba temporizada: si se agita (shake) el micro:bit mientras la cuenta regresiva está activa, el tiempo se reduce a la mitad. ¿Cómo modificarías tu diagrama de máquina de estados para incluir este nuevo evento y acción?

Rta//: Se que tengo que modificar el estado ARMED pero no se me ocurre como hacer para que se divida a la mitad


-Explica qué es un “vector de prueba” y por qué es una herramienta crucial para verificar que una máquina de estados funciona como se espera.

Rta//: Un vector de prueba es como una lista de pasos que usamos para ver si nuestro programa está funcionando bien. Por ejemplo, decimos: “si aprieto este botón cuando la bomba está esperando, debería pasar tal cosa”. Hacemos varias pruebas así para asegurarnos de que todo responda como debería. Es útil porque no tenemos que adivinar si está bien, sino que lo comprobamos paso a paso.


-¿Qué parte del diseño de la bomba temporizada te resultó más desafiante: crear el diagrama de estados (Actividad 04) o traducir ese diagrama a código MicroPython (Actividad 05)? ¿Por qué?

Rta//: Creo que la parte que mas me resulto desafiante fue la actividad 04, porque no tenia muy claro como organizar la informacióny mostrarla


-Describe un error o “bug” que encontraste al implementar tu programa. ¿Cómo te ayudó pensar en términos de estados, eventos y transiciones a identificar y solucionar el problema?

Rta//: Un error común que encontré fue que al presionar el botón para aumentar el tiempo (UP), el contador subía más de una vez con una sola pulsación. Esto pasaba porque el programa detectaba el botón como presionado durante varios ciclos seguidos. Pensar en términos de estados, eventos y transiciones me ayudó a entender que necesitaba un estado intermedio que esperara a que el botón se soltara antes de volver a permitir el aumento de tiempo. Así, agregué una condición para detectar el cambio de “no presionado” a “presionado”, y eso evitó que el contador subiera varias veces con un solo toque. Pensar en “qué está pasando” (evento), “en qué momento está el programa” (estado) y “qué debe hacer después” (transición), me permitió organizar mejor la lógica y resolver el problema.


-El problema de la bomba era complejo. ¿Qué estrategia usaste para abordarlo? ¿Comenzaste con una versión simple y añadiste funcionalidades poco a poco?

Rta//: Traté primero entenderlo para poder saber que partes iba a implementar primero, sabia que no iba a poder añadir todo a la vez, y conforme algo me funcionaba añadia otra cosa de poco para no dañar nada


-Ahora que entiendes el patrón de máquina de estados, ¿En qué otro tipo de proyecto o sistema de entretenimiento digital crees que podrías aplicarlo?

Rta//: Ahora que entiendo el patrón de máquina de estados, creo que podría aplicarlo en un videojuego interactivo, por ejemplo, un juego tipo plataforma donde el personaje cambia de estado: caminando, saltando, atacando o recibiendo daño. Cada una de esas acciones sería un estado diferente, y las teclas que el jugador presiona serían los eventos que hacen que el personaje cambie de estado.
