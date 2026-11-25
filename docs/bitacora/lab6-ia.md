He leído la política de uso de IA de la asignatura.

Declaración de uso de IA · Lab 6 · E047

Entrada 1 — Parte A: introducción y planificación del Lab 6

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): Venga ahora toca este laboratorio ayúdame, resúmela y ayúdame paso a paso como los otros
- Código recibido: No aplica.
- Dónde lo usé: Introducción y planificación del Lab 6.
- Propósito: Comprender los objetivos del laboratorio y organizar su realización por partes.
- Qué hace (con mis palabras): Preparé el entorno de Oracle para el laboratorio, organicé las prácticas por partes y creé una copia de seguridad inicial como punto de recuperación ante posibles fallos al modificar parámetros, permisos o almacenamiento. Con esta planificación entendí que administrar una base de datos no consiste solo en ejecutar consultas, sino también en supervisar su estado, gestionar recursos, controlar accesos y resolver incidencias.
- Evidencia de ejecución: No aplica.

Entrada 2 — Parte B.1: lista de turno

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original de la conversación]
- Código recibido: bash scripts/ops/ro.sh scripts/ops/turno.sql | tee "$EVID_LAB6/script/$(ts)_01-turno.script.log"
- Dónde lo usé: Parte B.1, lista de turno del DBA.
- Propósito: Comprobar el estado general de Oracle y registrar los resultados.
- Qué hace (con mis palabras): Ejecuté turno.sql para hacer una revisión inicial del estado de Oracle, como la que haría un DBA al empezar su jornada para detectar fallos antes de que afecten a los usuarios. El script comprueba si la instancia y la PDB están abiertas, si la base está en modo ARCHIVELOG, el estado del almacenamiento y de los archivos de control, las sesiones bloqueadas y los errores recientes del registro de alertas.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log

Entrada 3 — Parte B.2: mantenimiento automático

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/ro.sh scripts/lab6/01-automatizacion.sql freepdb1
- Dónde lo usé: Parte B.2, automatización de Oracle.
- Propósito: Revisar las tareas automáticas, las ventanas de mantenimiento, los umbrales, AWR y Scheduler.
- Qué hace (con mis palabras): Comprobé qué tareas de mantenimiento ejecuta Oracle de forma automática y en qué horarios. Vi cómo Oracle recopila estadísticas, analiza el espacio y estudia mejoras de rendimiento sin intervención manual constante, además de revisar las ventanas de mantenimiento y cómo se programan las tareas mediante el Scheduler.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log

Entrada 4 — Parte B: diagnóstico de errores ORA

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: Consulta SQL sobre V$DIAG_ALERT_EXT, agrupando mensajes mediante REGEXP_SUBSTR(message_text, 'ORA-[0-9]{5}').
- Dónde lo usé: Diagnóstico complementario de la Parte B.
- Propósito: Identificar los códigos de los seis errores detectados durante la lista de turno.
- Qué hace (con mis palabras): Consulté V$DIAG_ALERT_EXT filtrando y agrupando los errores ORA- del registro de alertas. Identifiqué seis errores ORA-00800, causados por intentos de cambiar la prioridad de procesos dentro del entorno Docker, comprobando así que ver errores en el alert log no significa automáticamente que la base haya fallado, sino que hay que analizar su causa e impacto.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log

Entrada 5 — Parte C.1: parámetros y SPFILE

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/lab6/02-pfile-so.sh preparar, bash scripts/ops/sysdba.sh scripts/lab6/02-parametros.sql ... y bash scripts/lab6/02-pfile-so.sh comparar.
- Dónde lo usé: Parte C.1, parámetros de inicialización.
- Propósito: Comprobar el comportamiento de los parámetros estáticos y las diferencias entre memoria, SPFILE y PFILE.
- Qué hace (con mis palabras): Comprobé cómo almacena y modifica Oracle sus parámetros de configuración: V$PARAMETER muestra los valores en uso y V$SPPARAMETER los guardados para el arranque. Probando con db_files (de valor 200 a 250), verifiqué que SCOPE=MEMORY intenta aplicar el cambio en memoria, SCOPE=SPFILE lo guarda para el siguiente reinicio y RESET elimina la configuración explícita del SPFILE (sin recuperar necesariamente el valor anterior).
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T182533Z_02-parametros.script.log y docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_spfile.ora

Entrada 6 — Parte C.2: estados de FREEPDB1

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/lab6/02-estados-pdb.sh | tee "$EVID_LAB6/script/$(ts)_02-estados-pdb.script.log"
- Dónde lo usé: Parte C.2, modos de apertura de una PDB.
- Propósito: Comprobar los estados READ ONLY, RESTRICTED, MOUNTED y READ WRITE.
- Qué hace (con mis palabras): Cambié los estados de apertura de FREEPDB1 para ver cómo afectan a los usuarios: READ WRITE permite consultar y modificar, READ ONLY solo consultar, RESTRICTED limita las conexiones a usuarios autorizados y MOUNTED deja la PDB montada sin abrir para trabajo normal. También comprobé que sin SAVE STATE aparece ORA-01109 tras reiniciar, mientras que guardar el estado permite recuperar la apertura automáticamente.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T182735Z_02-estados-pdb.script.log

Entrada 7 — Parte C.3: validación del arranque

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/ro.sh scripts/ops/validar-arranque.sql freepdb1
- Dónde lo usé: Parte C.3, validación posterior al reinicio.
- Propósito: Comprobar que FREEPDB1 se encuentra abierta y que sus servicios están activos.
- Qué hace (con mis palabras): Verifiqué que Oracle quedó operativo tras el reinicio revisando el estado de la instancia, la apertura de FREEPDB1, los servicios de conexión y los archivos necesarios. Sirve para confirmar que no basta con que el contenedor esté encendido: la base y sus servicios también deben estar disponibles para las aplicaciones.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T183104Z_02-validar-pdb.script.log

Entrada 8 — Parte D.1: servicio academia_app

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/sysdba.sh scripts/lab6/03-servicio.sql ...
- Dónde lo usé: Parte D.1, administración de servicios.
- Propósito: Crear y verificar el servicio de conexión de la aplicación Academia.
- Qué hace (con mis palabras): Creé y activé el servicio específico academia_app mediante DBMS_SERVICE para que la aplicación se conecte usando su propio nombre de servicio. Después comprobé que figuraba entre los servicios activos y anunciado por el listener, verificando que una base abierta no sirve a la aplicación si su servicio no está disponible.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T183227Z_03-servicio.script.log

Entrada 9 — Parte D.2: usuario de aplicación

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: Comprobación de APP_ACADEMIA_PWD en config/.env y ejecución de bash scripts/lab6/03-cuenta-app.sh.
- Dónde lo usé: Parte D.2, creación de usuarios locales.
- Propósito: Configurar la contraseña y crear la cuenta APP_ACADEMIA.
- Qué hace (con mis palabras): Configuré la cuenta local APP_ACADEMIA con los permisos necesarios para que la aplicación trabaje, evitando conceder privilegios administrativos innecesarios. La contraseña se almacenó en config/.env (fuera de Git) para separar las cuentas de aplicación de las administrativas y proteger las credenciales.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T183551Z_03-cuenta-app.script.log

Entrada 10 — Parte D.3: gestión de sesiones

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/lab6/03-sesiones.sh | tee "$EVID_LAB6/script/$(ts)_03-sesiones.script.log"
- Dónde lo usé: Parte D.3, observación y finalización de sesiones.
- Propósito: Identificar una sesión con una transacción abierta y comprobar el funcionamiento de CANCEL SQL y KILL SESSION.
- Qué hace (con mis palabras): Identifiqué una sesión activa y su proceso para comparar dos formas de intervención: CANCEL SQL cancela únicamente la sentencia en ejecución pero puede dejar la transacción abierta, mientras que KILL SESSION finaliza la sesión completa y provoca el ROLLBACK de los cambios pendientes. Así comprobé que conviene revisar qué está haciendo una sesión antes de cerrarla.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T183652Z_03-sesiones.script.log

Entrada 11 — Parte E.1: tres perspectivas del diccionario

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/lab6/04-tres-miradas.sh
- Dónde lo usé: Parte E.1, visibilidad del diccionario de Oracle.
- Propósito: Comparar la información accesible para diferentes usuarios y contenedores.
- Qué hace (con mis palabras): Ejecuté consultas equivalentes con distintos usuarios y contenedores para comprobar que la visibilidad depende tanto de los permisos como del contenedor actual: USER_ muestra los objetos propios, ALL_ los accesibles, DBA_ la información administrativa y CDB_ la información de los distintos contenedores.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log

Entrada 12 — Parte E.2: vistas del diccionario

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/ro.sh scripts/lab6/04-diccionario.sql
- Dónde lo usé: Parte E.2, exploración del diccionario.
- Propósito: Comprender el origen de las vistas dinámicas y localizar información sobre cuotas y permisos.
- Qué hace (con mis palabras): Exploré las vistas internas del diccionario de Oracle para conocer su origen y localizar información sobre cuotas y operaciones reanudables: las tablas X$ son estructuras internas, V$ son vistas dinámicas de rendimiento, GV$ son vistas globales útiles con varias instancias y los sinónimos públicos permiten consultarlas con nombres más sencillos.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log

Entrada 13 — Parte E.3: estadísticas y deltas

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/sysdba.sh scripts/lab6/04-deltas.sql ...
- Dónde lo usé: Parte E.3, medición del rendimiento.
- Propósito: Medir el coste de diez recorridos completos sobre la tabla PEDIDO.
- Qué hace (con mis palabras): Medí el coste real de las consultas comparando los contadores antes y después de la ejecución (deltas), ya que los contadores de Oracle son acumulativos. De este modo evalué el consumo específico de lecturas lógicas, DB time y DB CPU de la operación en lugar de leer totales acumulados.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T190230Z_04-deltas.script.log

Entrada 14 — Parte F.1: almacenamiento y cuotas

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/sysdba.sh scripts/lab6/05-almacenamiento.sql ...
- Dónde lo usé: Parte F.1, configuración del almacenamiento.
- Propósito: Crear un tablespace con crecimiento limitado y comprobar los errores por falta de cuota.
- Qué hace (con mis palabras): Creé el tablespace TBS_ACADEMIA_HIST con 10 MB iniciales y un máximo de 40 MB, configuré alertas de ocupación al 80 % y 95 % y probé los límites de cuota. Comprobé que el espacio libre del tablespace y la cuota del usuario son independientes: aunque haya espacio disponible, un usuario recibe ORA-01950 o ORA-01536 si no tiene cuota suficiente.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log

Entrada 15 — Parte F.2: operaciones reanudables

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/lab6/05-resumable.sh | tee "$EVID_LAB6/script/$(ts)_05-resumable.script.log"
- Dónde lo usé: Parte F.2, operaciones RESUMABLE.
- Propósito: Comprobar cómo Oracle suspende una carga por falta de cuota y la reanuda después de ampliar el espacio permitido.
- Qué hace (con mis palabras): Lancé una inserción de 20.000 registros con cuota insuficiente para el propietario de la tabla. En lugar de abortar con error, Oracle dejó la operación en estado SUSPENDED y, al ampliar la cuota de 2 MB a 30 MB dentro del tiempo permitido, la carga se reanudó automáticamente sin tener que repetirla desde cero.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T190520Z_05-resumable.script.log

Entrada 16 — Parte F.3: HWM y SHRINK SPACE

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Pegar mensaje original]
- Código recibido: bash scripts/ops/sysdba.sh scripts/lab6/05-hwm-shrink.sql ...
- Dónde lo usé: Parte F.3, recuperación de espacio.
- Propósito: Comprobar qué ocurre con el almacenamiento después de eliminar registros y compactar una tabla.
- Qué hace (con mis palabras): Inserté 20.000 filas, borré la mayoría hasta dejar 2.000 y comprobé que DELETE no libera automáticamente el espacio asignado porque el segmento mantiene la marca de agua alta (HWM). Al habilitar ROW MOVEMENT y ejecutar SHRINK SPACE, compacté la tabla y reduje el tamaño del segmento aproximadamente de 23 MB a 2,4 MB.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T190646Z_05-hwm-shrink.script.log

Entrada 17 — Parte G.1: perfiles y gobierno del acceso

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje original del chat donde compartiste los resultados de 06-gobierno-acceso]
- Código recibido: Comandos para ejecutar y comprobar los scripts de gobierno del acceso de la Parte G.
- Dónde lo usé: Parte G.1, perfiles de seguridad, roles y cuentas de usuario.
- Propósito: Comprobar la creación de PRF_PERSONAS, los roles funcionales y la cuenta ANA_GARCIA.
- Qué hace (con mis palabras): Creé el perfil de seguridad PRF_PERSONAS (que restringe intentos fallidos, tiempos de bloqueo y vigencia de contraseñas), los roles funcionales para agrupar permisos según tareas y la cuenta personal ANA_GARCIA, aplicando así el principio de conceder solo los permisos necesarios para cada función.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log

Entrada 18 — Parte G.2: pruebas de permisos

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia tu mensaje original con las pruebas de permisos de Ana y de la aplicación]
- Código recibido: Indicaciones para ejecutar y revisar las pruebas de acceso de la Parte G.
- Dónde lo usé: Parte G.2, validación de privilegios.
- Propósito: Comprobar que los usuarios podían realizar únicamente las operaciones autorizadas.
- Qué hace (con mis palabras): Probé tanto operaciones permitidas como prohibidas para validar los roles: comprobé que ANA_GARCIA podía consultar matrículas y modificar el ESTADO de un estudiante, pero no cambiar su nombre. Los errores ORA-41900 y ORA-00942 confirmaron que las restricciones funcionaban según lo esperado.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T193411Z_06-probar-acceso.script.log

Entrada 19 — Parte G.3: revocación en cascada

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje original donde compartiste el resultado de 06-cascada.sh]
- Código recibido: bash scripts/lab6/06-cascada.sh
- Dónde lo usé: Parte G.3, administración y revocación de privilegios.
- Propósito: Entender las diferencias entre ADMIN OPTION y GRANT OPTION.
- Qué hace (con mis palabras): Comprobé qué ocurre al revocar privilegios delegados a terceros: con ADMIN OPTION (privilegios de sistema), revocar al intermediario no hace que sus destinatarios pierdan el privilegio automáticamente; en cambio, con GRANT OPTION (privilegios de objeto), la revocación sí se propaga en cascada a los demás usuarios.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T193525Z_06-cascada.script.log

Entrada 20 — Parte H.1: objetos inválidos

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia tu mensaje de la Parte H con los resultados de 07-objetos]
- Código recibido: Indicaciones de ejecución y comprobación de scripts/lab6/07-objetos.sql.
- Dónde lo usé: Parte H.1, dependencias e índices.
- Propósito: Comprender la invalidación de vistas y funciones después de cambios en tablas.
- Qué hace (con mis palabras): Modifiqué columnas de tablas para ver cómo los cambios estructurales invalidan vistas y funciones dependientes, y cómo recompilarlos. También comprobé qué implica que un índice pase a estado UNUSABLE y cómo recuperarlo mediante su reconstrucción.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T193803Z_07-objetos.script.log

Entrada 21 — Parte H.2: memoria y advisors

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje donde compartiste las estadísticas de memoria]
- Código recibido: Indicaciones para revisar los resultados de scripts/lab6/07-memoria.sql.
- Dónde lo usé: Parte H.2, SGA, PGA y advisors de memoria.
- Propósito: Interpretar las recomendaciones de Oracle sobre la memoria de la instancia.
- Qué hace (con mis palabras): Analicé la SGA (1.536 MB) y la PGA objetivo (512 MB, con 0 sobreasignaciones) mediante las vistas de los advisors de memoria. Comprobé que duplicar la SGA no aportaba una mejora apreciable en el rendimiento estimado, por lo que no estaba justificado aumentar su tamaño.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T193912Z_07-memoria.script.log

Entrada 22 — Parte H.3: archivos críticos

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje donde compartiste el inventario de archivos de Oracle]
- Código recibido: Indicaciones para ejecutar y revisar scripts/lab6/07-archivos-criticos.sql.
- Dónde lo usé: Parte H.3, inventario y recuperación de la base.
- Propósito: Identificar archivos de control, redo logs, SPFILE, archivos archivados y copias RMAN.
- Qué hace (con mis palabras): Revisé el inventario de archivos esenciales para el funcionamiento y la recuperación de Oracle: los control files (estructura de la base), los redo logs (cambios para recuperación), los archived logs (secuencias de redo conservadas), las copias gestionadas por RMAN y el uso de la FRA como zona de almacenamiento para recuperación.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T194055Z_07-archivos-criticos.script.log

Entrada 23 — Parte H.4: ADR y trazas

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje donde mostraste los resultados de ADR y TKPROF]
- Código recibido: Indicaciones para ejecutar y analizar la práctica 07-adr-trazas.
- Dónde lo usé: Parte H.4, diagnóstico y trazado de sesiones.
- Propósito: Investigar los mensajes del alert log y analizar el coste de una consulta.
- Qué hace (con mis palabras): Consulté el repositorio de diagnóstico ADR (donde se centralizan alertas y trazas para investigar errores) y analicé una traza de sesión con TKPROF para medir el coste de una consulta. En la prueba se registraron 249 lecturas lógicas, de las cuales 247 correspondieron a la fase de FETCH.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T194227Z_07-adr-trazas.script.log

Entrada 24 — Parte I.2: incidente INC-601

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje original donde compartiste el diagnóstico del bloqueo de INC-601]
- Código recibido: Orientaciones para consultar las sesiones bloqueadas y ejecutar ALTER SYSTEM KILL SESSION '206,970' IMMEDIATE; después de comprobar SID y SERIAL#.
- Dónde lo usé: Parte I.2, incidente INC-601.
- Propósito: Localizar y resolver un bloqueo de transacción.
- Qué hace (con mis palabras): Investigué por qué Ana García no podía guardar la ficha del estudiante 101 y descubrí que otra sesión mantenía una transacción bloqueando esa fila. Localicé el SID y SERIAL# de la sesión bloqueadora y la finalicé de forma selectiva en lugar de reiniciar la instancia.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261124T194614Z_08-incidente1-diagnostico.script.log y docs/bitacora/lab6/evidencia/script/20261124T194729Z_08-incidente1-validacion.script.log

Entrada 25 — Parte I.3: incidente INC-602

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje original donde mostraste el ticket ORA-12514 y el diagnóstico del listener]
- Código recibido: bash scripts/lab6/08-guardia.sh incidente 2, ejecución de 08-diagnostico.sql y recuperación del servicio mediante scripts/lab6/03-servicio.sql.
- Dónde lo usé: Parte I.3, incidente INC-602.
- Propósito: Identificar y corregir un problema de conexión con el servicio academia_app.
- Qué hace (con mis palabras): Diagnostiqué un error ORA-12514 con la base de datos abierta: el servicio academia_app existía pero estaba detenido y no aparecía en el listener. Arranqué el servicio y validé que la aplicación volvía a conectarse, comprobando que un error de conexión puede deberse a un servicio concreto y no a una caída de Oracle.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261125T114623Z_08-incidente2-diagnostico.script.log, docs/bitacora/lab6/evidencia/script/20261125T114930Z_08-incidente2-intervencion.script.log y docs/bitacora/lab6/evidencia/script/20261125T114936Z_08-incidente2-validacion.script.log

Entrada 26 — Parte I.4: incidente INC-603

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje original donde compartiste el diagnóstico de APP_ACADEMIA bloqueada]
- Código recibido: Consulta de DBA_USERS y sentencia ALTER USER app_academia ACCOUNT UNLOCK;.
- Dónde lo usé: Parte I.4, incidente INC-603.
- Propósito: Identificar el bloqueo administrativo de la cuenta de aplicación y recuperar su acceso.
- Qué hace (con mis palabras): Ante el error ORA-28000, comprobé en DBA_USERS que la cuenta APP_ACADEMIA estaba en estado LOCKED (bloqueo administrativo, distinto de LOCKED(TIMED) por intentos fallidos). Desbloqueé únicamente esa cuenta y validé la reconexión de la aplicación, entendiendo por qué hay que proteger estas cuentas frente a procesos automáticos de bajas.
- Evidencia de ejecución: docs/bitacora/lab6/evidencia/script/20261125T115039Z_08-incidente3-diagnostico.script.log y docs/bitacora/lab6/evidencia/script/20261125T115132Z_08-incidente3-validacion.script.log

Entrada 27 — Parte J: preguntas de comprobación

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): Dame las 20 preguntas corregidas con los errores que tengo que añadir
- Código recibido: No aplica.
- Dónde lo usé: Parte J.2, preparación de lab6-respuestas.md.
- Propósito: Recibir una guía con explicaciones y correcciones para las 20 preguntas del laboratorio, interpretar los resultados de las consultas y localizar las evidencias correspondientes.
- Qué hace (con mis palabras): Utilicé la guía con las explicaciones de las 20 respuestas que me proporcionó ChatGPT para revisar mis resultados, corregir errores, estructurar las explicaciones y enlazar cada respuesta con su evidencia real en los registros del laboratorio, comprobando que las respuestas técnicas deben justificarse con datos obtenidos en la práctica.
- Evidencia de ejecución: No aplica. Documento relacionado: docs/bitacora/lab6-respuestas.md

Entrada 28 — Parte J: verificación y preparación de la entrega

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): Si ya está bien sigamos que hay que acabar
- Código recibido: bash scripts/lab6/09-verificacion-final.sh y comandos de comprobación de Git.
- Dónde lo usé: Parte J.1 y J.3, verificación técnica y preparación de la entrega.
- Propósito: Detectar requisitos pendientes antes de crear el commit final y el Pull Request.
- Qué hace (con mis palabras): Ejecuté 09-verificacion-final.sh para auditar el estado completo de la entrega (base de datos, archivos, evidencias, permisos y documentación). La primera ejecución detectó un fallo porque faltaba lab6-respuestas.md; tras crearlo y repetir la verificación, obtuve RESULTADO: TODO OK. Lab 6 listo para entregar.
- Evidencia de ejecución: Primera verificación (1 fallo): docs/bitacora/lab6/evidencia/script/20261125T120617Z_09-verificacion-final.script.log. Segunda verificación (RESULTADO: TODO OK, 25/11/2026, 12:32:14 UTC): [PEGAR LA RUTA EXACTA DEL LOG 09 FINAL; encontrarla con grep -l "RESULTADO: TODO OK" docs/bitacora/lab6/evidencia/script/*_09-verificacion-final.script.log].

Entrada 29 — Recuperación del entorno Docker

- Herramienta: ChatGPT
- Prompt (literal, copiado tal cual): [Copia el mensaje donde mostraste que Docker no estaba disponible desde WSL]
- Código recibido: Comandos de comprobación de Docker Desktop y docker start "$CONT_NAME".
- Dónde lo usé: Recuperación del entorno antes de continuar con la Parte I.
- Propósito: Volver a iniciar Oracle sin eliminar el contenedor ni perder los datos.
- Qué hace (con mis palabras): Al volver al laboratorio, Ubuntu no encontraba el comando docker y Oracle no respondía. Recuperé la integración de Docker Desktop con WSL, comprobé el contenedor y arranqué oralab-26ai sin perder datos: verifiqué que FREEPDB1 seguía en READ WRITE, el estudiante 101 continuaba ACTIVO y el histórico mantenía los 2.000 registros.
- Evidencia de ejecución: docs/bitacora/lab6/incidencias-entorno/20261125T114332Z_docker-no-disponible.log
