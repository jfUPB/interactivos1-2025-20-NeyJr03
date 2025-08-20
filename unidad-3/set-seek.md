# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 05

Modelo de la bomba 3.0

La bomba 3.0 se basa en una máquina de estados que recibe eventos genéricos (provenientes de botones, puerto serial o p5.js). Esto permite que la lógica de la bomba sea independiente de la fuente del evento y escalable a múltiples interfaces de control.

Estados principales:

 1. Configuración

- Estado inicial.

- Se puede ajustar el tiempo de la bomba (10 a 60 seg).

- Eventos válidos: UP, DOWN, ARMED.

 2. Armada (Cuenta regresiva)

- Inicia la cuenta regresiva.

- Se puede desactivar con la secuencia A-B-A.

- Si la secuencia es incorrecta, continúa el conteo.

- Eventos válidos: DISARM_SEQ, TIMEOUT, TOUCH.

 3. Explosión

- Estado terminal cuando el contador llega a 0.

- Acción: encender speaker.

 4. Desarmada

- Se regresa a este estado si la secuencia de desarme es correcta o si se toca el botón de touch.

- Acción: reinicia el contador y pasa a Configuración.


Tabla de vectores de prueba


| Estado inicial | Evento disparador         | Acciones realizadas                        | Estado final  |
| -------------- | ------------------------- | ------------------------------------------ | ------------- |
| Configuración  | `UP`                      | Incrementar el tiempo (+1 seg)             | Configuración |
| Configuración  | `DOWN`                    | Decrementar el tiempo (–1 seg)             | Configuración |
| Configuración  | `ARMED`                   | Iniciar cuenta regresiva en display        | Armada        |
| Armada         | `DISARM_SEQ (A-B-A)`      | Validar secuencia y detener cuenta         | Desarmada     |
| Armada         | `DISARM_SEQ (Incorrecta)` | Mostrar error / continuar cuenta regresiva | Armada        |
| Armada         | `TIMEOUT`                 | Encender speaker → explosión               | Explosión     |
| Armada         | `TOUCH`                   | Forzar reinicio y regresar a configuración | Configuración |
| Desarmada      | —                         | Reiniciar contador a valor configurado     | Configuración |
| Explosión      | —                         | Mantener alarma encendida                  | Explosión     |




