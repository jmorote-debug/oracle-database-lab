He leído la política de uso de IA de la asignatura.

# Declaración de uso de IA · Lab 6 · E047

<!--
CÓMO SE RELLENA (léelo y borra este comentario si quieres; el script de evaluación lo ignora)
- La PRIMERA línea es obligatoria y no se toca: «He leído la política de uso de IA de la asignatura.»
- Copia este archivo como docs/bitacora/lab6-ia.md (junto a lab6-respuestas.md) y pon tu código en el título.
  Cada laboratorio tiene el suyo: en el Lab 7 será docs/bitacora/lab7-ia.md.
- Si NO has usado IA: deja solo la línea «No he usado IA.» y borra la entrada de ejemplo.
- Si la has usado: borra la línea «No he usado IA.» y escribe UNA entrada por cada uso, con los 7 campos.
  Un campo vacío es una entrada incompleta (D3: −0,5 por entrada).
- Preguntar a la IA como tutor o corregir la ortografía de un texto propio está permitido: decláralo también.
  Si no copiaste código, escribe «no aplica» en «Código recibido» y en «Evidencia de ejecución» (no cuentan como vacíos).
  Los demás campos son siempre obligatorios.
- Una entrada con TODOS los campos vacíos (la de ejemplo sin tocar) no cuenta: se ignora.
- El código copiado de una IA puntúa si lo EJECUTAS en tu contenedor, lo EXPLICAS con tus palabras,
  dices para qué lo usaste y adjuntas aquí el código y el prompt LITERAL.
-->

## Entrada 1

- **Herramienta:** ChatGPT

- **Prompt (literal, copiado tal cual):**
  Ayúdame con el laboratorio VI de esta asignatura, resúmela y ayúdame paso a paso.

- **Código recibido:** No aplica.

- **Dónde lo usé:** Introducción y planificación del Lab 6.

- **Propósito:** Comprender los objetivos del laboratorio y organizar su realización por partes.

- **Qué hace (con mis palabras):**
 En el apartado A: He preparado un entorno y creado una copia para recuperarlo si algo falla.
 En el apartado B: He aprendido a saber si un la base de datos funciona correctamente y qué mantenimiento hace Oracle por si solo.
 En el apartado C: He aprendido como afectan los parametros al funcionamiento y cómo conseguir que una PDB se abra automáticamente al reiniciar.

- **Evidencia de ejecución:** No aplica

## Entrada 2 — Parte B.1: lista de turno

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original de la conversación]
- **Código recibido (fragmento o ruta):** `bash scripts/ops/ro.sh scripts/ops/turno.sql | tee "$EVID_LAB6/script/$(ts)_01-turno.script.log"`
- **Dónde lo usé:** Parte B.1, lista de turno del DBA.
- **Propósito:** Comprobar el estado general de Oracle y registrar los resultados.
- **Qué hace (con mis palabras):** [Explicar las comprobaciones de instancia, PDB, almacenamiento, bloqueos y alertas]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log`

## Entrada 3 — Parte B.2: mantenimiento automático

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/ro.sh scripts/lab6/01-automatizacion.sql freepdb1`
- **Dónde lo usé:** Parte B.2, automatización de Oracle.
- **Propósito:** Revisar las tareas automáticas, las ventanas de mantenimiento, los umbrales, AWR y Scheduler.
- **Qué hace (con mis palabras):** [Explicar qué comprueba el script y qué significan los resultados]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log`

## Entrada 4 — Parte B: diagnóstico de errores ORA

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** Consulta SQL sobre `V$DIAG_ALERT_EXT`, agrupando mensajes mediante `REGEXP_SUBSTR(message_text, 'ORA-[0-9]{5}')`.
- **Dónde lo usé:** Diagnóstico complementario de la Parte B.
- **Propósito:** Identificar los códigos de los seis errores detectados durante la lista de turno.
- **Qué hace (con mis palabras):** [Explicar cómo se filtran y agrupan los errores del último día]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log`

## Entrada 5 — Parte C.1: parámetros y SPFILE

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/lab6/02-pfile-so.sh preparar`, `bash scripts/ops/sysdba.sh scripts/lab6/02-parametros.sql ...` y `bash scripts/lab6/02-pfile-so.sh comparar`.
- **Dónde lo usé:** Parte C.1, parámetros de inicialización.
- **Propósito:** Comprobar el comportamiento de los parámetros estáticos y las diferencias entre memoria, SPFILE y PFILE.
- **Qué hace (con mis palabras):** [Explicar SCOPE=MEMORY, SCOPE=SPFILE, RESET y las copias de parámetros]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T182533Z_02-parametros.script.log`
- **Evidencia adicional:** `docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_spfile.ora`

## Entrada 6 — Parte C.2: estados de FREEPDB1

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/lab6/02-estados-pdb.sh | tee "$EVID_LAB6/script/$(ts)_02-estados-pdb.script.log"`
- **Dónde lo usé:** Parte C.2, modos de apertura de una PDB.
- **Propósito:** Comprobar los estados READ ONLY, RESTRICTED, MOUNTED y READ WRITE.
- **Qué hace (con mis palabras):** [Explicar el efecto de DISCARD STATE y SAVE STATE durante los reinicios]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T182735Z_02-estados-pdb.script.log`

## Entrada 7 — Parte C.3: validación del arranque

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/ro.sh scripts/ops/validar-arranque.sql freepdb1`
- **Dónde lo usé:** Parte C.3, validación posterior al reinicio.
- **Propósito:** Comprobar que FREEPDB1 se encuentra abierta y que sus servicios están activos.
- **Qué hace (con mis palabras):** [Explicar las comprobaciones de instancia, PDB, servicios, alert log y datafiles]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T183104Z_02-validar-pdb.script.log`

## Entrada 8 — Parte D.1: servicio academia_app

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/sysdba.sh scripts/lab6/03-servicio.sql ...`
- **Dónde lo usé:** Parte D.1, administración de servicios.
- **Propósito:** Crear y verificar el servicio de conexión de la aplicación Academia.
- **Qué hace (con mis palabras):** [Explicar la creación, activación y verificación del servicio mediante el listener]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T183227Z_03-servicio.script.log`

## Entrada 9 — Parte D.2: usuario de aplicación

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** Comprobación de `APP_ACADEMIA_PWD` en `config/.env` y ejecución de `bash scripts/lab6/03-cuenta-app.sh`.
- **Dónde lo usé:** Parte D.2, creación de usuarios locales.
- **Propósito:** Configurar la contraseña y crear la cuenta APP_ACADEMIA.
- **Qué hace (con mis palabras):** [Explicar cómo se configura la contraseña sin mostrarla y qué permisos recibe el usuario]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T183551Z_03-cuenta-app.script.log`

## Entrada 10 — Parte D.3: gestión de sesiones

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/lab6/03-sesiones.sh | tee "$EVID_LAB6/script/$(ts)_03-sesiones.script.log"`
- **Dónde lo usé:** Parte D.3, observación y finalización de sesiones.
- **Propósito:** Identificar una sesión con una transacción abierta y comprobar el funcionamiento de CANCEL SQL y KILL SESSION.
- **Qué hace (con mis palabras):** [Explicar la diferencia entre cancelar una llamada y finalizar una sesión, y qué ocurre con el ROLLBACK]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T183652Z_03-sesiones.script.log`

## Entrada 11 — Parte E.1: tres perspectivas del diccionario

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/lab6/04-tres-miradas.sh`
- **Dónde lo usé:** Parte E.1, visibilidad del diccionario de Oracle.
- **Propósito:** Comparar la información accesible para diferentes usuarios y contenedores.
- **Qué hace (con mis palabras):** [Explicar las diferencias entre USER_, ALL_, DBA_ y CDB_]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log`

## Entrada 12 — Parte E.2: vistas del diccionario

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/ro.sh scripts/lab6/04-diccionario.sql`
- **Dónde lo usé:** Parte E.2, exploración del diccionario.
- **Propósito:** Comprender el origen de las vistas dinámicas y localizar información sobre cuotas y permisos.
- **Qué hace (con mis palabras):** [Explicar qué son las tablas X$, las vistas V$ y GV$, y los sinónimos públicos]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log`

## Entrada 13 — Parte E.3: estadísticas y deltas

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/sysdba.sh scripts/lab6/04-deltas.sql ...`
- **Dónde lo usé:** Parte E.3, medición del rendimiento.
- **Propósito:** Medir el coste de diez recorridos completos sobre la tabla PEDIDO.
- **Qué hace (con mis palabras):** [Explicar cómo se obtienen los deltas y qué representan DB time, DB CPU y las lecturas lógicas]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T190230Z_04-deltas.script.log`

## Entrada 14 — Parte F.1: almacenamiento y cuotas

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/sysdba.sh scripts/lab6/05-almacenamiento.sql ...`
- **Dónde lo usé:** Parte F.1, configuración del almacenamiento.
- **Propósito:** Crear un tablespace con crecimiento limitado y comprobar los errores por falta de cuota.
- **Qué hace (con mis palabras):** [Explicar el tamaño inicial, el máximo permitido, las cuotas y los umbrales de alerta]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log`

## Entrada 15 — Parte F.2: operaciones reanudables

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/lab6/05-resumable.sh | tee "$EVID_LAB6/script/$(ts)_05-resumable.script.log"`
- **Dónde lo usé:** Parte F.2, operaciones RESUMABLE.
- **Propósito:** Comprobar cómo Oracle suspende una carga por falta de cuota y la reanuda después de ampliar el espacio permitido.
- **Qué hace (con mis palabras):** [Explicar por qué aparece SUSPENDED, cómo se amplía la cuota y cómo continúa la inserción]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T190520Z_05-resumable.script.log`

## Entrada 16 — Parte F.3: HWM y SHRINK SPACE

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Pegar mensaje original]
- **Código recibido:** `bash scripts/ops/sysdba.sh scripts/lab6/05-hwm-shrink.sql ...`
- **Dónde lo usé:** Parte F.3, recuperación de espacio.
- **Propósito:** Comprobar qué ocurre con el almacenamiento después de eliminar registros y compactar una tabla.
- **Qué hace (con mis palabras):** [Explicar por qué DELETE no reduce el segmento y qué hacen ROW MOVEMENT y SHRINK SPACE]
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T190646Z_05-hwm-shrink.script.log`
