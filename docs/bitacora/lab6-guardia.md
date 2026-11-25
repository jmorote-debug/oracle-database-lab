## INC-601 · Bloqueo al guardar una ficha de estudiante

**Detección:** El 24/11/2026, a las 19:46 UTC, secretaría notificó que Ana García no podía guardar la ficha del estudiante 101 porque la aplicación se quedaba bloqueada.

**Impacto:** La operación de guardado no podía completarse. No se conoce la duración total de la incidencia, pero el bloqueo quedó registrado durante el diagnóstico.

**Diagnóstico:** Al consultar `V$SESSION` y `V$LOCK`, observé que la sesión 48, perteneciente a `ANA_GARCIA`, estaba esperando un bloqueo `enq: TX - row lock contention`. La sesión que lo provocaba era la 206, correspondiente a `APP_ACADEMIA`.

**Causa raíz:** [Explica con tus palabras por qué una transacción que permanece abierta puede impedir que otro usuario modifique el mismo registro.]

**Intervención:** Después de comprobar el SID y el SERIAL# de la sesión bloqueadora, ejecuté:

`ALTER SYSTEM KILL SESSION '206,970' IMMEDIATE;`

[Explica por qué decidiste terminar únicamente esa sesión y no reiniciar la base de datos.]

**Validación:** Volví a ejecutar el diagnóstico y comprobé que ya no aparecían sesiones bloqueadas. También consulté el estudiante 101 y confirmé que su estado era `ACTIVO`.

**Acción preventiva:** [Propón cómo evitar que una aplicación mantenga transacciones abiertas durante demasiado tiempo y cómo detectar bloqueos similares antes de que afecten a los usuarios.]
Incidente	Problema			Solución
INC-601		Bloqueo de una fila		Finalizar la sesión bloqueadora
INC-602		Servicio academia_app detenido	Arrancar el servicio
INC-603		Cuenta APP_ACADEMIA bloqueada	Desbloquear la cuenta
