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

## Entrada 17 — Parte G.1: perfiles y gobierno del acceso

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje original del chat donde compartiste los resultados de 06-gobierno-acceso].
- **Código recibido:** Comandos para ejecutar y comprobar los scripts de gobierno del acceso de la Parte G.
- **Dónde lo usé:** Parte G.1, perfiles de seguridad, roles y cuentas de usuario.
- **Propósito:** Comprobar la creación de `PRF_PERSONAS`, los roles funcionales y la cuenta `ANA_GARCIA`.
- **Qué hace (con mis palabras):** [Explica cómo el perfil limita intentos de acceso y cómo los roles permiten asignar permisos sin concederlos individualmente].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log`

## Entrada 18 — Parte G.2: pruebas de permisos

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia tu mensaje original con las pruebas de permisos de Ana y de la aplicación].
- **Código recibido:** Indicaciones para ejecutar y revisar las pruebas de acceso de la Parte G.
- **Dónde lo usé:** Parte G.2, validación de privilegios.
- **Propósito:** Comprobar que los usuarios podían realizar únicamente las operaciones autorizadas.
- **Qué hace (con mis palabras):** [Explica por qué Ana podía consultar las matrículas y modificar ESTADO, pero no NOMBRES, y por qué algunos errores eran esperados].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T193411Z_06-probar-acceso.script.log`

## Entrada 19 — Parte G.3: revocación en cascada

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje original donde compartiste el resultado de 06-cascada.sh].
- **Código recibido:** `bash scripts/lab6/06-cascada.sh`
- **Dónde lo usé:** Parte G.3, administración y revocación de privilegios.
- **Propósito:** Entender las diferencias entre `ADMIN OPTION` y `GRANT OPTION`.
- **Qué hace (con mis palabras):** [Explica qué ocurrió al revocar un privilegio de sistema y uno de objeto, y por qué sus efectos sobre terceros fueron distintos].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T193525Z_06-cascada.script.log`

## Entrada 20 — Parte H.1: objetos inválidos

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia tu mensaje de la Parte H con los resultados de 07-objetos].
- **Código recibido:** Indicaciones de ejecución y comprobación de `scripts/lab6/07-objetos.sql`.
- **Dónde lo usé:** Parte H.1, dependencias e índices.
- **Propósito:** Comprender la invalidación de vistas y funciones después de cambios en tablas.
- **Qué hace (con mis palabras):** [Explica cómo una modificación de columna puede invalidar objetos dependientes, cómo se recompilan y qué significa un índice UNUSABLE].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T193803Z_07-objetos.script.log`

## Entrada 21 — Parte H.2: memoria y advisors

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje donde compartiste las estadísticas de memoria].
- **Código recibido:** Indicaciones para revisar los resultados de `scripts/lab6/07-memoria.sql`.
- **Dónde lo usé:** Parte H.2, SGA, PGA y advisors de memoria.
- **Propósito:** Interpretar las recomendaciones de Oracle sobre la memoria de la instancia.
- **Qué hace (con mis palabras):** [Explica cómo comparaste distintos tamaños de SGA y PGA y por qué los resultados no justificaban aumentar la memoria].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T193912Z_07-memoria.script.log`

## Entrada 22 — Parte H.3: archivos críticos

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje donde compartiste el inventario de archivos de Oracle].
- **Código recibido:** Indicaciones para ejecutar y revisar `scripts/lab6/07-archivos-criticos.sql`.
- **Dónde lo usé:** Parte H.3, inventario y recuperación de la base.
- **Propósito:** Identificar archivos de control, redo logs, SPFILE, archivos archivados y copias RMAN.
- **Qué hace (con mis palabras):** [Explica la función de los archivos de control y redo, y qué información proporciona la FRA].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T194055Z_07-archivos-criticos.script.log`

## Entrada 23 — Parte H.4: ADR y trazas

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje donde mostraste los resultados de ADR y TKPROF].
- **Código recibido:** Indicaciones para ejecutar y analizar la práctica `07-adr-trazas`.
- **Dónde lo usé:** Parte H.4, diagnóstico y trazado de sesiones.
- **Propósito:** Investigar los mensajes del alert log y analizar el coste de una consulta.
- **Qué hace (con mis palabras):** [Explica para qué sirve ADR, cómo se identifica la traza de una sesión y qué significan las lecturas lógicas mostradas por TKPROF].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T194227Z_07-adr-trazas.script.log`

## Entrada 24 — Parte I.2: incidente INC-601

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje original donde compartiste el diagnóstico del bloqueo de INC-601].
- **Código recibido:** Orientaciones para consultar las sesiones bloqueadas y ejecutar `ALTER SYSTEM KILL SESSION '206,970' IMMEDIATE;` después de comprobar SID y SERIAL#.
- **Dónde lo usé:** Parte I.2, incidente INC-601.
- **Propósito:** Localizar y resolver un bloqueo de transacción.
- **Qué hace (con mis palabras):** [Explica cómo identificaste a la sesión bloqueadora y por qué terminaste esa sesión en lugar de reiniciar la instancia].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261124T194614Z_08-incidente1-diagnostico.script.log` y `20261124T194729Z_08-incidente1-validacion.script.log`

## Entrada 25 — Parte I.3: incidente INC-602

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje original donde mostraste el ticket ORA-12514 y el diagnóstico del listener].
- **Código recibido:** `bash scripts/lab6/08-guardia.sh incidente 2`, ejecución de `08-diagnostico.sql` y recuperación del servicio mediante `scripts/lab6/03-servicio.sql`.
- **Dónde lo usé:** Parte I.3, incidente INC-602.
- **Propósito:** Identificar y corregir un problema de conexión con el servicio `academia_app`.
- **Qué hace (con mis palabras):** [Explica por qué el servicio detenido producía ORA-12514, cómo se arrancó y cómo comprobaste que la aplicación podía conectarse].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261125T114623Z_08-incidente2-diagnostico.script.log`, `20261125T114930Z_08-incidente2-intervencion.script.log` y `20261125T114936Z_08-incidente2-validacion.script.log`

## Entrada 26 — Parte I.4: incidente INC-603

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje original donde compartiste el diagnóstico de APP_ACADEMIA bloqueada].
- **Código recibido:** Consulta de `DBA_USERS` y sentencia `ALTER USER app_academia ACCOUNT UNLOCK;`.
- **Dónde lo usé:** Parte I.4, incidente INC-603.
- **Propósito:** Identificar el bloqueo administrativo de la cuenta de aplicación y recuperar su acceso.
- **Qué hace (con mis palabras):** [Explica la diferencia entre LOCKED y LOCKED(TIMED), cómo desbloqueaste la cuenta y cómo validaste la conexión].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261125T115039Z_08-incidente3-diagnostico.script.log` y `20261125T115132Z_08-incidente3-validacion.script.log`

## Entrada 27 — Parte J: preguntas de comprobación

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** Dame las 20 preguntas corregidas con los errores que tengo que añadir
- **Código recibido:** No aplica.
- **Dónde lo usé:** Parte J.2, preparación de `lab6-respuestas.md`.
- **Propósito:** Revisar las respuestas del laboratorio, identificar errores y localizar las evidencias correspondientes.
- **Qué hace (con mis palabras):** [Explica qué respuestas revisaste, qué errores corregiste y cómo contrastaste los resultados con tus registros].
- **Evidencia de ejecución:** No aplica. Documento relacionado: `docs/bitacora/lab6-respuestas.md`.

## Entrada 28 — Parte J: verificación y preparación de la entrega

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** Si ya está bien sigamos que hay que acabar
- **Código recibido:** `bash scripts/lab6/09-verificacion-final.sh` y comandos de comprobación de Git.
- **Dónde lo usé:** Parte J.1 y J.3, verificación técnica y preparación de la entrega.
- **Propósito:** Detectar requisitos pendientes antes de crear el commit final y el Pull Request.
- **Qué hace (con mis palabras):** [Explica qué comprobó el verificador, qué fallo apareció inicialmente y cómo se resolvió al crear el documento de respuestas].
- **Evidencia de ejecución:** `docs/bitacora/lab6/evidencia/script/20261125T120617Z_09-verificacion-final.script.log` y la evidencia posterior de verificación con resultado `TODO OK`.

## Entrada 29 — Recuperación del entorno Docker

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** [Copia el mensaje donde mostraste que Docker no estaba disponible desde WSL].
- **Código recibido:** Comandos de comprobación de Docker Desktop y `docker start "$CONT_NAME"`.
- **Dónde lo usé:** Recuperación del entorno antes de continuar con la Parte I.
- **Propósito:** Volver a iniciar Oracle sin eliminar el contenedor ni perder los datos.
- **Qué hace (con mis palabras):** [Explica cómo se recuperó la integración de Docker con WSL y se comprobó que la PDB y los datos seguían disponibles].
- **Evidencia de ejecución:** `docs/bitacora/lab6/incidencias-entorno/20261125T114332Z_docker-no-disponible.log`
