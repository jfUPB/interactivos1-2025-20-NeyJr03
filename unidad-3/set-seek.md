# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 05

Modelo de la bomba 3.0

La bomba 3.0 se basa en una máquina de estados que recibe eventos genéricos (provenientes de botones, puerto serial o p5.js). Esto permite que la lógica de la bomba sea independiente de la fuente del evento y escalable a múltiples interfaces de control.

Estados principales:

Configuración

Estado inicial.

Se puede ajustar el tiempo de la bomba (10 a 60 seg).

Eventos válidos: UP, DOWN, ARMED.

Armada (Cuenta regresiva)

Inicia la cuenta regresiva.

Se puede desactivar con la secuencia A-B-A.

Si la secuencia es incorrecta, continúa el conteo.

Eventos válidos: DISARM_SEQ, TIMEOUT, TOUCH.

Explosión

Estado terminal cuando el contador llega a 0.

Acción: encender speaker.

Desarmada

Se regresa a este estado si la secuencia de desarme es correcta o si se toca el botón de touch.

Acción: reinicia el contador y pasa a Configuración.


