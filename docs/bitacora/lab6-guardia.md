## INC-601 · Bloqueo al guardar una ficha de estudiante

**Detección:** El 24/11/2026, a las 19:46 UTC, secretaría notificó que Ana García no podía guardar la ficha del estudiante 101 porque la aplicación se quedaba bloqueada.

**Impacto:** La operación de guardado no podía completarse. No se conoce la duración total de la incidencia, pero el bloqueo quedó registrado durante el diagnóstico.

**Diagnóstico:** Al consultar `V$SESSION` y `V$LOCK`, observé que la sesión 48, perteneciente a `ANA_GARCIA`, estaba esperando un bloqueo `enq: TX - row lock contention`. La sesión que lo provocaba era la 206, correspondiente a `APP_ACADEMIA`.


**Causa raíz:** APP_ACADEMIA mantenía una transacción sin finalizar y retenía el bloqueo de la fila que necesitaba modifica

**Intervención:** Después de comprobar el SID y el SERIAL# de la sesión bloqueadora, ejecuté:

`ALTER SYSTEM KILL SESSION '206,970' IMMEDIATE;`

Terminé únicamente la sesión bloqueadora 206,970 porque reiniciar la base afectaría a todos los usuarios y era innecesario.

**Validación:** Volví a ejecutar el diagnóstico y comprobé que ya no aparecían sesiones bloqueadas. También consulté el estudiante 101 y confirmé que su estado era `ACTIVO`.

**Acción preventiva:** Evitar que la aplicación mantenga transacciones abiertas demasiado tiempo; usar COMMIT o ROLLBACK cuando corresponda y alertar de bloqueos prolongados.

## INC-602 · Error de conexión ORA-12514

**Detección:** 25/11/2026, 11:46 UTC. Equipo de matrículas. Error ORA-12514.

**Impacto:** Ninguna instancia de la aplicación podía establecer nuevas conexiones.

**Diagnóstico:** 08-diagnostico.sql: academia_app = NO. En lsnrctl status no aparecía el servicio.

**Causa raíz:** El servicio academia_app estaba detenido, aunque Oracle y el listener funcionaban. No se comprobó el motivo original de la parada.

**Intervención:** DBMS_SERVICE.START_SERVICE('academia_app') y posteriormente SAVE STATE

**Validación:** academia_app = SI, listener READY y conexión de APP_ACADEMIA correcta, con 17.600 estudiantes consultados.

**Acción preventiva:** Monitorizar que academia_app esté activo y anunciado por el listener.


## INC-603 · Cuenta de aplicación bloqueada

**Detección:** 	25/11/2026, 11:50 UTC. Equipo de matrículas. Error ORA-28000 después de un despliegue.

**Impacto:** La aplicación no podía iniciar sesión con su cuenta de base de datos. 

**Diagnóstico:** DBA_USERS: APP_ACADEMIA = LOCKED, perfil DEFAULT, 10 intentos permitidos.

**Causa raíz:** Bloqueo administrativo de la cuenta. El ticket apunta al script trimestral de bajas como posible origen, pero no está confirmado mediante su revisión.

**Intervención:** ALTER USER app_academia ACCOUNT UNLOCK;

**Validación:** Cuenta OPEN, conexión correcta, 17.600 estudiantes consultados y una actualización de prueba deshecha con ROLLBACK.

**Acción preventiva:** Excluir las cuentas de aplicación del script automático de bajas y revisar previamente las cuentas afectadas.
