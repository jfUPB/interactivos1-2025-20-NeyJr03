# Unidad 3


## 🤔 Fase: Reflect

### Actividad 08

- Parte 1: Recuperación de conocimiento

1. ¿Qué es una máquina de estados y cuáles son sus cuatro componentes?
Una máquina de estados es como una forma de organizar un programa por pasos o “estados” que cambian dependiendo de lo que pase. En lugar de que todo sea un montón de instrucciones seguidas, se va moviendo de un estado a otro según las condiciones.
Los cuatro componentes que usamos en esta unidad son:

- Los estados en los que puede estar el sistema (ejemplo: CONFIG, ARMED, EXPLOTO).

- Los eventos o entradas que hacen que algo cambie (ejemplo: presionar A o B en el micro:bit).

- Las acciones que se ejecutan al recibir esos eventos (ejemplo: aumentar el tiempo, iniciar la bomba, mostrar el BOOM).

- Y las transiciones, que son los pasos que conectan un estado con otro cuando ocurre un evento.

- (Al comienzo pensé que también se contaba el “tiempo” como un componente, pero en realidad eso es más una variable de apoyo).

2. ¿Por qué son útiles para manejar concurrencia en un solo hilo como micro:bit o p5.js?
La máquina de estados es muy útil porque permite que un programa atienda varias cosas “a la vez”, aunque en realidad el micro:bit o p5.js solo hace una cosa por turno. Lo que pasa es que, al tener cada estado bien definido, el programa revisa rápidamente qué debe hacer en cada momento sin quedarse “pegado” en una tarea.
Esto soluciona un problema grande cuando uno usa funciones como sleep(), porque si el programa se duerme, deja de escuchar todo lo demás. En cambio, con la máquina de estados, el flujo sigue corriendo y se pueden detectar botones, entradas o tiempo sin bloquear nada.

3. ¿Cómo modificarías el diagrama si se reduce el tiempo a la mitad con un nuevo evento?
Yo añadiría un nuevo evento, digamos “HACK” (podría ser un comando serial o una combinación rara de botones). Este evento se detectaría solo cuando la bomba está en el estado ARMED. Entonces, en el diagrama, dentro de ARMED habría una transición adicional que al recibir “HACK” manda la acción de dividir el tiempo en dos. No cambiaría de estado, seguiría en ARMED, solo que el contador pasaría a ser más corto.

(Para no complicarlo demasiado, lo pondría como una flecha que regresa de ARMED a ARMED con la etiqueta “HACK → tiempo/2”).

4. ¿Qué es un vector de prueba y por qué es importante?
Un vector de prueba es como una lista de entradas que uno prepara para asegurarse de que la máquina de estados responde bien en cada caso. Es como un guion de “si hago esto, debería pasar esto otro”.
Por ejemplo, si presiono A y luego B, el vector de prueba dice qué debería pasar con el tiempo y con el estado. Es importante porque ayuda a verificar que el sistema funcione como lo planeamos y que no se nos escape algún error.
Yo al principio pensé que era solo como una simulación gráfica, pero en realidad se usa más como una tabla de casos para revisar que no haya fallos.




- Parte 2: reflexión sobre tu proceso (Metacognición)

1. Para mi fue complicado armar el diagrama como tal, pero la parte mas dificil fué implementar eso al código y que funcionara correctamente


2. Un bug que me ocurrió fue que el temporizador no se reiniciaba bien cuando volvía al estado de configuración. A veces la bomba arrancaba con el tiempo viejo en lugar de volver a 20. Me di cuenta que era porque no estaba reseteando la variable tiempo al cambiar de estado. Lo solucioné agregando la instrucción para reiniciar el contador justo en la transición a "CONFIG".


3. Lo que hice fué ir paso a paso y me fui guiando poco a poco con lo que ya tenia y lo que tenía que hacer 

4. Creo que la técnica de máquina de estados también se puede aplicar en un videojuego sencillo, por ejemplo un juego de plataformas. Allí se podrían manejar estados como “quieto”, “corriendo”, “saltando” o “cayendo”. Esto ayuda a que el personaje reaccione de forma ordenada según lo que haga el jugador, sin que todo se mezcle o se ejecute al mismo tiempo. Me parece útil porque evita errores cuando hay muchas acciones y además hace más fácil añadir nuevas funciones después, como un “ataque especial” o un “poder”.




### Actividad 09

1. El ejemplo de la bomba me pareció excelente para poner en práctica los conocimientos que ibamos viendo en la unidad, siempre fué complejo pero aun asi sirivio irle añadiendo cosas al tema de la bomba


2. Tal vez en algun momento me sentí algo perdido pero logré encontrar el camino correcto


3. Tal vez alguna guía mas visual o algo que me ayude a saber por donde ir


4. 4, siempre tiene su nivel de dificultad pero estoy seguro que habrán cosas más dificiles


5. Nada en específico, solo decir que en varios momentos me sentí algo frustrado, pero logré resolverlo



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





