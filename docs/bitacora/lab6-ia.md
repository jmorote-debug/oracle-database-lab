He leído la política de uso de IA de la asignatura.

# Declaración de uso de IA · Lab 6 · E047

## Entrada 1 — Parte A: introducción y planificación del Lab 6

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** Venga ahora toca este laboratorio ayúdame, resúmela y ayúdame paso a paso como los otros
- **Código recibido:** No aplica.
- **Dónde lo usé:** Introducción y planificación del Lab 6.
- **Propósito:** Comprender los objetivos del laboratorio y organizar su realización por partes.
- **Qué hace (con mis palabras):** Preparé el entorno de Oracle para el laboratorio, organicé las prácticas por partes y creé una copia de seguridad inicial como punto de recuperación ante posibles fallos al modificar parámetros, permisos o almacenamiento. Con esta planificación entendí que administrar una base de datos no consiste solo en ejecutar consultas, sino también en supervisar su estado, gestionar recursos, controlar accesos y resolver incidencias.
- **Evidencia de ejecución:** No aplica.

## Entrada 2 — Parte B.1: lista de turno

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

# Eliminar espacios sobrantes al final de las líneas
sed -i 's/[[:blank:]]\+$//' \
  docs/bitacora/lab6-ia.md \
  docs/plantillas/IA.md \
  scripts/lab6/02-parametros.sql \
  scripts/lab6/03-sesiones.sh

# Actualizar los archivos preparados para el commit
git add \
  docs/bitacora/lab6-ia.md \
  docs/plantillas/IA.md \
  scripts/lab6/02-parametros.sql \
  scripts/lab6/03-sesiones.sh

# Verificar de nuevo
echo "===== COMPROBACIÓN DE FORMATO ====="
git --no-pager diff --cached --check

echo "===== ARCHIVOS PREPARADOS ====="
git --no-pager diff --cached --stat
===== COMPROBACIÓN DE FORMATO =====
===== ARCHIVOS PREPARADOS =====
 config/.env.example                              |   3 +
 docs/bitacora/lab6-ia.md                         |  37 +++
 ...1124T171152Z_00-backup-lab6-inicio.script.log |  84 ++++++
 docs/plantillas/IA.md                            |  36 +++
 login.sql                                        |   4 +
 scripts/deployment/env/00-config.sh              |   2 +
 scripts/lab6/01-automatizacion.sql               |  54 ++++
 scripts/lab6/02-estados-pdb.sh                   |  88 ++++++
 scripts/lab6/02-parametros.sql                   |  35 +++
 scripts/lab6/02-pfile-so.sh                      |  23 ++
 scripts/lab6/03-cuenta-app.sh                    |  10 +
 scripts/lab6/03-cuenta-app.sql                   |  31 ++
 scripts/lab6/03-servicio.sql                     |  35 +++
 scripts/lab6/03-sesiones.sh                      | 100 +++++++
 scripts/lab6/04-deltas.sql                       |  62 ++++
 scripts/lab6/04-diccionario.sql                  |  42 +++
 scripts/lab6/04-tres-miradas.sh                  |  12 +
 scripts/lab6/04-tres-miradas.sql                 |  19 ++
 scripts/lab6/05-almacenamiento.sql               |  76 +++++
 scripts/lab6/05-hwm-shrink.sql                   |  23 ++
 scripts/lab6/05-resumable.sh                     |  65 ++++
 scripts/lab6/06-app-sigue.sql                    |  12 +
 scripts/lab6/06-cascada.sh                       |  54 ++++
 scripts/lab6/06-gobierno-acceso.sh               |   9 +
 scripts/lab6/06-gobierno-acceso.sql              |  83 ++++++
 scripts/lab6/06-probar-acceso.sh                 |  33 ++
 scripts/lab6/06-sesion-ana.sql                   |  21 ++
 scripts/lab6/07-adr-trazas.sh                    |  59 ++++
 scripts/lab6/07-archivos-criticos.sql            |  31 ++
 scripts/lab6/07-memoria.sql                      |  35 +++
 scripts/lab6/07-objetos.sql                      |  75 +++++
 scripts/lab6/08-diagnostico.sql                  |  49 +++
 scripts/lab6/08-guardia.sh                       |  80 +++++
 scripts/lab6/09-verificacion-final.sh            |  97 ++++++
 scripts/ops/alumno.sh                            |  41 +++
 scripts/ops/app.sh                               |  17 ++
 scripts/ops/autoria.py                           | 298 +++++++++++++++++++
 scripts/ops/backup-estado.sh                     |   5 +-
 scripts/ops/cabecera.sh                          |  30 ++
 scripts/ops/cabecera.sql                         |  16 +
 scripts/ops/ro.sh                                |   7 +-
 scripts/ops/sysdba.sh                            |   3 +-
 scripts/ops/turno.sql                            |  35 +++
 scripts/ops/validar-arranque.sql                 |  34 +++
 44 files changed, 1959 insertions(+), 6 deletions(-)
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git add docs/bitacora/lab6-ia.md
git --no-pager diff --cached --check
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "chore(ops): add Lab 6 kit, AI declaration and starting backup" \
  -m "Refs #8"

echo "===== ÚLTIMO COMMIT ====="
git log -1 --oneline

echo "===== ESTADO DE LA RAMA ====="
git status -sb
[chore/6-administracion-operativa be55c4a] chore(ops): add Lab 6 kit, AI declaration and starting backup
 44 files changed, 1959 insertions(+), 6 deletions(-)
 create mode 100644 docs/bitacora/lab6-ia.md
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T171152Z_00-backup-lab6-inicio.script.log
 create mode 100644 docs/plantillas/IA.md
 create mode 100644 login.sql
 create mode 100644 scripts/lab6/01-automatizacion.sql
 create mode 100755 scripts/lab6/02-estados-pdb.sh
 create mode 100644 scripts/lab6/02-parametros.sql
 create mode 100755 scripts/lab6/02-pfile-so.sh
 create mode 100755 scripts/lab6/03-cuenta-app.sh
 create mode 100644 scripts/lab6/03-cuenta-app.sql
 create mode 100644 scripts/lab6/03-servicio.sql
 create mode 100755 scripts/lab6/03-sesiones.sh
 create mode 100644 scripts/lab6/04-deltas.sql
 create mode 100644 scripts/lab6/04-diccionario.sql
 create mode 100755 scripts/lab6/04-tres-miradas.sh
 create mode 100644 scripts/lab6/04-tres-miradas.sql
 create mode 100644 scripts/lab6/05-almacenamiento.sql
 create mode 100644 scripts/lab6/05-hwm-shrink.sql
 create mode 100755 scripts/lab6/05-resumable.sh
 create mode 100644 scripts/lab6/06-app-sigue.sql
 create mode 100755 scripts/lab6/06-cascada.sh
 create mode 100755 scripts/lab6/06-gobierno-acceso.sh
 create mode 100644 scripts/lab6/06-gobierno-acceso.sql
 create mode 100755 scripts/lab6/06-probar-acceso.sh
 create mode 100644 scripts/lab6/06-sesion-ana.sql
 create mode 100755 scripts/lab6/07-adr-trazas.sh
 create mode 100644 scripts/lab6/07-archivos-criticos.sql
 create mode 100644 scripts/lab6/07-memoria.sql
 create mode 100644 scripts/lab6/07-objetos.sql
 create mode 100644 scripts/lab6/08-diagnostico.sql
 create mode 100755 scripts/lab6/08-guardia.sh
 create mode 100755 scripts/lab6/09-verificacion-final.sh
 create mode 100755 scripts/ops/alumno.sh
 create mode 100755 scripts/ops/app.sh
 create mode 100644 scripts/ops/autoria.py
 mode change 100644 => 100755 scripts/ops/backup-estado.sh
 create mode 100755 scripts/ops/cabecera.sh
 create mode 100644 scripts/ops/cabecera.sql
 mode change 100644 => 100755 scripts/ops/ro.sh
 mode change 100644 => 100755 scripts/ops/sysdba.sh
 create mode 100644 scripts/ops/turno.sql
 create mode 100644 scripts/ops/validar-arranque.sql
===== ÚLTIMO COMMIT =====
be55c4a (HEAD -> chore/6-administracion-operativa) chore(ops): add Lab 6 kit, AI declaration and starting backup
===== ESTADO DE LA RAMA =====
## chore/6-administracion-operativa
?? scripts/ops/__pycache__/
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/ro.sh scripts/ops/turno.sql | tee "$EVID_LAB6/script/$(ts)_01-turno.script.log"
- **Dónde lo usé:** Parte B.1, lista de turno del DBA.
- **Propósito:** Comprobar el estado general de Oracle y registrar los resultados.
- **Qué hace (con mis palabras):** Ejecuté turno.sql para hacer una revisión inicial del estado de Oracle, como la que haría un DBA al empezar su jornada para detectar fallos antes de que afecten a los usuarios. El script comprueba si la instancia y la PDB están abiertas, si la base está en modo ARCHIVELOG, el estado del almacenamiento y de los archivos de control, las sesiones bloqueadas y los errores recientes del registro de alertas.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log

## Entrada 3 — Parte B.2: mantenimiento automático

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** **jorge@Jorge \~/oracle-database-lab (chore/6-administracion-operativa)**\
**$ cd \~/oracle-database-lab**\
\
**# Evitar que Git detecte cachés de Python**\
**grep -qxF '\_\_pycache\_\_/' .gitignore ||**\&#xA;**&#x20; printf '\n# Cachés de Python\n__pycache\_\_/\n' >> .gitignore**\
\
**# Verificar que ya se ignora**\
**git check-ignore scripts/ops/\_\_pycache\_\_/**\
\
**git status -sb**\
**scripts/ops/\_\_pycache\_\_/**\
**## chore/6-administracion-operativa**\&#xA;**&#x20;M .gitignore**\
**jorge@Jorge \~/oracle-database-lab (chore/6-administracion-operativa)**\
**$ cd \~/oracle-database-lab**\
\
**source scripts/deployment/env/00-config.sh**\
\
**mkdir -p "$EVID_LAB6"/{script,spool,config}**\
\
**echo "===== LISTA DE TURNO DEL DBA ====="**\
\
**bash scripts/ops/ro.sh scripts/ops/turno.sql \\**\&#xA;**&#x20; | tee "$EVID_LAB6/script/$(ts)\_01-turno.script.log"**\
**===== LISTA DE TURNO DEL DBA =====**\
**== EVIDENCIA alumno=E047 hora=2026-11-24T18:21:34Z origen=turno**\
**== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553466**\
**== 1. ¿Dónde estoy y quién soy? ==**\
\
**CONTENEDOR   USUARIO      AHORA**\
**------------ ------------ --------------------**\
**CDB$ROOT     C##OPS_RO    2026-11-24 18:21 UTC**\
**== 2. ¿Instancia y base están como deben? ==**\
\
**INSTANCIA  ESTADO       LOGINS     ARRANQUE**\
**---------- ------------ ---------- ----------------**\
**FREE       OPEN         ALLOWED    2026-11-24 17:15**\
\
**NAME       OPEN_MODE  LOG_MODE**\
**---------- ---------- ----------**\
**FREE       READ WRITE ARCHIVELOG**\
**== 3. ¿Están abiertas las PDB? ==**\
\&#xA;**&#x20;   CON_ID NAME       OPEN_MODE  RESTRICTED**\
**---------- ---------- ---------- ----------**\&#xA;**&#x20;        2 PDB$SEED   READ ONLY  NO**\&#xA;**&#x20;        3 FREEPDB1   READ WRITE NO**\
**== 4. ¿Cuántos errores ORA- hay en el alert log en las últimas 24 h? (compáralo con tu línea base) ==**\
\
**ERRORES_ORA_24H**\
**---------------**\&#xA;**&#x20;             6**\
**== 5. ¿Algún tablespace por encima del 85 % de su máximo? (vacío = bien) ==**\
**== 6. ¿Hay sesiones bloqueadas ahora mismo? ==**\
\
**SESIONES_BLOQUEADAS**\
**-------------------**\&#xA;**&#x20;                 0**\
**== 7. ¿Hay alertas del servidor pendientes? ==**\
\
**ALERTAS_PENDIENTES**\
**------------------**\&#xA;**&#x20;                0**\
**jorge@Jorge \~/oracle-database-lab (chore/6-administracion-operativa)**\
**$ echo "===== EVIDENCIA 01 ====="**\
\
**ls -lh "$EVID_LAB6/script/"\*\_01-turno.script.log**\
\
**echo "===== CABECERA DE LA EVIDENCIA ====="**\
\
**head -n 3 "$(ls -t "$EVID_LAB6/script/"\*\_01-turno.script.log | head -1)"**\
**===== EVIDENCIA 01 =====**\
**-rw-r--r-- 1 jorge jorge 1.3K Nov 24 19:21 docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log**\
**===== CABECERA DE LA EVIDENCIA =====**\
**== EVIDENCIA alumno=E047 hora=2026-11-24T18:21:34Z origen=turno**\
**== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553466**\
**== 1. ¿Dónde estoy y quién soy? ==**\
**jorge@Jorge \~/oracle-database-lab (chore/6-administracion-operativa)**\
**$**
- **Código recibido:** bash scripts/ops/ro.sh scripts/lab6/01-automatizacion.sql freepdb1
- **Dónde lo usé:** Parte B.2, automatización de Oracle.
- **Propósito:** Revisar las tareas automáticas, las ventanas de mantenimiento, los umbrales, AWR y Scheduler.
- **Qué hace (con mis palabras):** Comprobé qué tareas de mantenimiento ejecuta Oracle de forma automática y en qué horarios. Vi cómo Oracle recopila estadísticas, analiza el espacio y estudia mejoras de rendimiento sin intervención manual constante, además de revisar las ventanas de mantenimiento y cómo se programan las tareas mediante el Scheduler.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log

## Entrada 4 — Parte B: diagnóstico de errores ORA

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PARTE B.2: AUTOMATIZACIÓN ORACLE ====="

bash scripts/ops/ro.sh \
  scripts/lab6/01-automatizacion.sql \
  freepdb1
===== PARTE B.2: AUTOMATIZACIÓN ORACLE =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:22:35Z origen=01-automatizacion
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553532
== EVIDENCIA alumno=E047 hora=2026-11-24T18:22:37Z origen=01-automatizacion
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553543
== 1. Tareas de mantenimiento automático (AutoTask) ==

CLIENT_NAME                      STATUS   WINDOW_GROUP
-------------------------------- -------- ----------------
auto optimizer stats collection  ENABLED  ORA$AT_WGRP_OS
auto space advisor               ENABLED  ORA$AT_WGRP_SA
sql tuning advisor               ENABLED  ORA$AT_WGRP_SQ
== 2. Ventanas de mantenimiento: cuándo y cuántas horas duran ==

WINDOW_NAME       REPEAT_INTERVAL                                                        HORAS ENABLED
----------------- ---------------------------------------------------------------------- ----- -------
FRIDAY_WINDOW     freq=daily;byday=FRI;byhour=22;byminute=0;bysecond=0                       4 TRUE
MONDAY_WINDOW     freq=daily;byday=MON;byhour=22;byminute=0;bysecond=0                       4 TRUE
SATURDAY_WINDOW   freq=daily;byday=SAT;byhour=6;byminute=0;bysecond=0                       20 TRUE
SUNDAY_WINDOW     freq=daily;byday=SUN;byhour=6;byminute=0;bysecond=0                       20 TRUE
THURSDAY_WINDOW   freq=daily;byday=THU;byhour=22;byminute=0;bysecond=0                       4 TRUE
TUESDAY_WINDOW    freq=daily;byday=TUE;byhour=22;byminute=0;bysecond=0                       4 TRUE
WEDNESDAY_WINDOW  freq=daily;byday=WED;byhour=22;byminute=0;bysecond=0                       4 TRUE
WEEKEND_WINDOW    freq=daily;byday=SAT;byhour=0;byminute=0;bysecond=0                       48 FALSE
WEEKNIGHT_WINDOW  freq=daily;byday=MON,TUE,WED,THU,FRI;byhour=22;byminute=0;bysecond=0       8 FALSE
== 3. Umbrales de las alertas de espacio (MMON) que rigen EN ESTA PDB ==
(NONE = ningún umbral: MMON no avisará aunque el tablespace se llene; se arregla en la Parte F)

TABLESPACE     OP           AVISO         CRITICO
-------------- ------------ ------------- -------------
SYSTEM         NONE
TBS_ACADEMIA   NONE
TBS_TIENDASUR  NONE
TEMP           DO NOT CHECK (automático)  0
UNDOTBS1       DO NOT CHECK (automático)  0
USERS          NONE
== 4. AWR: cada cuánto toma fotos y cuánto las guarda ==

SNAP_INTERVAL        RETENTION
-------------------- --------------------
+00 01:00:00.000000  +08 00:00:00.000000

NAME                             VALOR
-------------------------------- --------------------
statistics_level                 TYPICAL
control_management_pack_access   DIAGNOSTIC+TUNING
== 5. Trabajos del Scheduler: cuántos hay y cuántos fallaron en 7 días ==

OWNER        TRABAJOS HABILITADOS
---------- ---------- -----------
SYS                24          12
ORDS_METAD          1           1
ATA

(vacío en la última consulta = ningún trabajo falló en 7 días)
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== EVIDENCIA DE AUTOMATIZACIÓN ====="

ls -lh "$EVID_LAB6/spool/"*_01-automatizacion.spool.log

echo "===== CABECERA ====="

head -n 3 "$(
  ls -t "$EVID_LAB6/spool/"*_01-automatizacion.spool.log |
  head -1
)"
===== EVIDENCIA DE AUTOMATIZACIÓN =====
-rw-r--r-- 1 jorge jorge 3.1K Nov 24 19:22 docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log
===== CABECERA =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:22:37Z origen=01-automatizacion
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553543
SQL Format Cleared
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Consulta SQL sobre V$DIAG_ALERT_EXT, agrupando mensajes mediante REGEXP_SUBSTR(message_text, 'ORA-[0-9]{5}').
- **Dónde lo usé:** Diagnóstico complementario de la Parte B.
- **Propósito:** Identificar los códigos de los seis errores detectados durante la lista de turno.
- **Qué hace (con mis palabras):** Consulté V$DIAG_ALERT_EXT filtrando y agrupando los errores ORA- del registro de alertas. Identifiqué seis errores ORA-00800, causados por intentos de cambiar la prioridad de procesos dentro del entorno Docker, comprobando así que ver errores en el alert log no significa automáticamente que la base haya fallado, sino que hay que analizar su causa e impacto.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log

## Entrada 5 — Parte C.1: parámetros y SPFILE

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

TEMP_SQL=$(mktemp /tmp/lab6-ora-XXXXXX.sql)

cat > "$TEMP_SQL" <<'SQL'
SET LINESIZE 160 PAGESIZE 100
COLUMN CODIGO FORMAT A12
COLUMN EJEMPLO FORMAT A100

SELECT REGEXP_SUBSTR(message_text, 'ORA-[0-9]{5}') AS codigo,
       COUNT(*) AS veces,
       SUBSTR(MIN(message_text), 1, 100) AS ejemplo
FROM v$diag_alert_ext
WHERE originating_timestamp > SYSTIMESTAMP - INTERVAL '1' DAY
  AND message_text LIKE '%ORA-%'
GROUP BY REGEXP_SUBSTR(message_text, 'ORA-[0-9]{5}')
ORDER BY veces DESC;
SQL

bash scripts/ops/ro.sh "$TEMP_SQL" \
  | tee "$EVID_LAB6/script/$(ts)_01-errores-ora.script.log"

rm -f "$TEMP_SQL"
== EVIDENCIA alumno=E047 hora=2026-11-24T18:23:32Z origen=lab6-ora-sauUIt
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553588

CODIGO          VECES EJEMPLO
____________ ________ _______________________________________________________________________________________________________
ORA-00800           6 Errors in file /opt/oracle/diag/rdbms/free/FREE/trace/FREE_lgwr_84.trc  (incident=25793) (PDBNAME=CD

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

git add \
  .gitignore \
  scripts/ops/turno.sql \
  scripts/lab6/01-automatizacion.sql \
  docs/bitacora/lab6-ia.md \
  "$EVID_LAB6/script/"*_01-* \
  "$EVID_LAB6/spool/"*_01-*

echo "===== COMPROBACIÓN ====="
git --no-pager diff --cached --check

echo "===== ARCHIVOS PREPARADOS ====="
git --no-pager diff --cached --stat
===== COMPROBACIÓN =====
docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log:5: trailing whitespace.
+CONTENEDOR   USUARIO      AHORA
docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log:10: trailing whitespace.
+INSTANCIA  ESTADO       LOGINS     ARRANQUE
docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log:14: trailing whitespace.
+NAME       OPEN_MODE  LOG_MODE
docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log:21: trailing whitespace.
+         2 PDB$SEED   READ ONLY  NO
docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log:22: trailing whitespace.
+         3 FREEPDB1   READ WRITE NO
docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log:4: trailing whitespace.
+CODIGO          VECES EJEMPLO
docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log:5: trailing whitespace.
+____________ ________ _______________________________________________________________________________________________________
docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log:6: trailing whitespace.
+ORA-00800           6 Errors in file /opt/oracle/diag/rdbms/free/FREE/trace/FREE_lgwr_84.trc  (incident=25793) (PDBNAME=CD
docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log:7: new blank line at EOF.
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:6: trailing whitespace.
+CLIENT_NAME                      STATUS   WINDOW_GROUP
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:8: trailing whitespace.
+auto optimizer stats collection  ENABLED  ORA$AT_WGRP_OS
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:9: trailing whitespace.
+auto space advisor               ENABLED  ORA$AT_WGRP_SA
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:10: trailing whitespace.
+sql tuning advisor               ENABLED  ORA$AT_WGRP_SQ
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:15: trailing whitespace.
+FRIDAY_WINDOW     freq=daily;byday=FRI;byhour=22;byminute=0;bysecond=0                       4 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:16: trailing whitespace.
+MONDAY_WINDOW     freq=daily;byday=MON;byhour=22;byminute=0;bysecond=0                       4 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:17: trailing whitespace.
+SATURDAY_WINDOW   freq=daily;byday=SAT;byhour=6;byminute=0;bysecond=0                       20 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:18: trailing whitespace.
+SUNDAY_WINDOW     freq=daily;byday=SUN;byhour=6;byminute=0;bysecond=0                       20 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:19: trailing whitespace.
+THURSDAY_WINDOW   freq=daily;byday=THU;byhour=22;byminute=0;bysecond=0                       4 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:20: trailing whitespace.
+TUESDAY_WINDOW    freq=daily;byday=TUE;byhour=22;byminute=0;bysecond=0                       4 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:21: trailing whitespace.
+WEDNESDAY_WINDOW  freq=daily;byday=WED;byhour=22;byminute=0;bysecond=0                       4 TRUE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:22: trailing whitespace.
+WEEKEND_WINDOW    freq=daily;byday=SAT;byhour=0;byminute=0;bysecond=0                       48 FALSE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:23: trailing whitespace.
+WEEKNIGHT_WINDOW  freq=daily;byday=MON,TUE,WED,THU,FRI;byhour=22;byminute=0;bysecond=0       8 FALSE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:27: trailing whitespace.
+TABLESPACE     OP           AVISO         CRITICO
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:29: trailing whitespace.
+SYSTEM         NONE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:30: trailing whitespace.
+TBS_ACADEMIA   NONE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:31: trailing whitespace.
+TBS_TIENDASUR  NONE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:32: trailing whitespace.
+TEMP           DO NOT CHECK (automático)  0
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:33: trailing whitespace.
+UNDOTBS1       DO NOT CHECK (automático)  0
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:34: trailing whitespace.
+USERS          NONE
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:37: trailing whitespace.
+SNAP_INTERVAL        RETENTION
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:39: trailing whitespace.
++00 01:00:00.000000  +08 00:00:00.000000
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:41: trailing whitespace.
+NAME                             VALOR
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:43: trailing whitespace.
+statistics_level                 TYPICAL
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:44: trailing whitespace.
+control_management_pack_access   DIAGNOSTIC+TUNING
docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log:51: trailing whitespace.
+ATA
===== ARCHIVOS PREPARADOS =====
 .gitignore                                       |  3 ++
 .../script/20261124T182134Z_01-turno.script.log  | 38 ++++++++++++++
 .../20261124T182331Z_01-errores-ora.script.log   |  7 +++
 .../20261124T182237Z_01-automatizacion.spool.log | 53 ++++++++++++++++++++
 4 files changed, 101 insertions(+)
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "docs(ops): add shift checklist and review automated maintenance" \
  -m "Refs #8"

git status -sb
git log -2 --oneline
[chore/6-administracion-operativa 6e6e0eb] docs(ops): add shift checklist and review automated maintenance
 4 files changed, 101 insertions(+)
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T182134Z_01-turno.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T182331Z_01-errores-ora.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/spool/20261124T182237Z_01-automatizacion.spool.log
## chore/6-administracion-operativa
6e6e0eb (HEAD -> chore/6-administracion-operativa) docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/02-pfile-so.sh preparar, bash scripts/ops/sysdba.sh scripts/lab6/02-parametros.sql ... y bash scripts/lab6/02-pfile-so.sh comparar.
- **Dónde lo usé:** Parte C.1, parámetros de inicialización.
- **Propósito:** Comprobar el comportamiento de los parámetros estáticos y las diferencias entre memoria, SPFILE y PFILE.
- **Qué hace (con mis palabras):** Comprobé cómo almacena y modifica Oracle sus parámetros de configuración: V$PARAMETER muestra los valores en uso y V$SPPARAMETER los guardados para el arranque. Probando con db_files (de valor 200 a 250), verifiqué que SCOPE=MEMORY intenta aplicar el cambio en memoria, SCOPE=SPFILE lo guarda para el siguiente reinicio y RESET elimina la configuración explícita del SPFILE (sin recuperar necesariamente el valor anterior).
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T182533Z_02-parametros.script.log y docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_spfile.ora

## Entrada 6 — Parte C.2: estados de FREEPDB1

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== ESTADO DE ORACLE ====="
bash scripts/ops/esperar-healthy.sh

echo "===== PARÁMETRO db_files ====="

docker exec -i "$CONT_NAME" sqlplus -s -L / as sysdba <<'SQL'
SET LINESIZE 150 PAGESIZE 50
COLUMN NAME FORMAT A20
COLUMN VALUE FORMAT A20
COLUMN ISSPECIFIED FORMAT A15
COLUMN ISSYS_MODIFIABLE FORMAT A20

SELECT name, value, isspecified
FROM v$spparameter
WHERE name = 'db_files'
  AND sid = '*';

SELECT name, value, issys_modifiable
FROM v$parameter
WHERE name = 'db_files';

EXIT
SQL
===== ESTADO DE ORACLE =====
  t=0s  docker=healthy  cdb/pdb=READWRITE/READWRITE
===== PARÁMETRO db_files =====

NAME                 VALUE                ISSPECIFIED
-------------------- -------------------- ---------------
db_files                                  FALSE


NAME                 VALUE                ISSYS_MODIFIABLE
-------------------- -------------------- --------------------
db_files             200                  FALSE

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PREPARAR COPIAS PFILE ====="

bash scripts/lab6/02-pfile-so.sh preparar
===== PREPARAR COPIAS PFILE =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:25:28Z origen=02-pfile-so
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553660
drwxr-xr-x 2 oracle oinstall 4096 Nov 24 18:25 /opt/oracle/oradata/lab6
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== PARTE C.1: PARÁMETROS Y SCOPE ====="

bash scripts/ops/sysdba.sh \
  scripts/lab6/02-parametros.sql \
  "$EVID_LAB6/script/$(ts)_02-parametros.script.log"
===== PARTE C.1: PARÁMETROS Y SCOPE =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:25:33Z origen=02-parametros
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553663
== 1. ¿Con qué archivo de parámetros arrancó la instancia? ==

NAME                   VALUE
---------------------- --------------------------------------------
spfile                 /opt/oracle/product/26ai/dbhomeFree/dbs/spfi
                       leFREE.ora


1 row selected.

== 2. Red de seguridad antes de tocar nada: el último estado bueno, en texto ==

File created.


File created.

== 3. Tipos de parámetro: estático (FALSE), dinámico inmediato, dinámico diferido; y si la PDB puede tener el suyo ==

NAME                   VALUE                                        ISSYS_MODIFIABLE ISPDB_MODIFIABLE
---------------------- -------------------------------------------- ---------------- ----------------
sort_area_size         65536                                        DEFERRED     TRUE
control_files          /opt/oracle/oradata/FREE/control01.ctl, /opt FALSE       FALSE
                       /oracle/oradata/FREE/control02.ctl, /opt/ora
                       cle/oradata/FREE/control03.ctl

db_files               200                                          FALSE       TRUE
db_recovery_file_dest_ 4294967296                                   IMMEDIATE            FALSE
size

resumable_timeout      0                                            IMMEDIATE            TRUE
undo_retention         900                                          IMMEDIATE            TRUE

6 rows selected.

== 4. Un parámetro ESTÁTICO no se puede cambiar en memoria (error esperado: ORA-02095) ==
ALTER SYSTEM SET db_files = 250 SCOPE = MEMORY
                 *
ERROR at line 1:
ORA-02095: specified initialization parameter cannot be modified
Help: https://docs.oracle.com/error-help/db/ora-02095/


== 5. Con SCOPE = SPFILE se acepta... pero solo vale en el próximo arranque ==

ORIGEN            VALUE                                        ISSPECIFIED
----------------- -------------------------------------------- -----------
SPFILE (antes)    (sin fijar)                                  FALSE

1 row selected.


System altered.


ORIGEN            VALUE                                        ISSPECIFIED
----------------- -------------------------------------------- -----------
SPFILE (archivo)  250                                          TRUE
MEMORIA (en uso)  200

2 rows selected.

== 6. Vuelta atrás. db_files NO estaba fijado (la copia del paso 2 no lo tiene): se deshace con RESET ==

System altered.


ORIGEN            VALUE                                        ISSPECIFIED
----------------- -------------------------------------------- -----------
SPFILE (después)  (sin fijar)                                  FALSE

1 row selected.

== 7. Desde una PDB no se cambia un parámetro del CDB (error esperado: ORA-65040) ==

Session altered.

ALTER SYSTEM SET processes = 250 SCOPE = SPFILE
*
ERROR at line 1:
ORA-65040: Operation is not allowed from within a pluggable database.
Help: https://docs.oracle.com/error-help/db/ora-65040/



Session altered.

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== COMPARACIÓN DE PFILES ====="

bash scripts/lab6/02-pfile-so.sh comparar
===== COMPARACIÓN DE PFILES =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:25:39Z origen=02-pfile-so
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7553803
  34 /opt/oracle/oradata/lab6/init_desde_spfile.ora
 126 /opt/oracle/oradata/lab6/init_desde_memoria.ora
 160 total
== Líneas del PFILE creado desde el SPFILE (lo que alguien fijó) ==
FREE.__data_transfer_cache_size=0
FREE.__datamemory_area_size=0
FREE.__db_cache_size=973078528
FREE.__inmemory_ext_roarea=0
FREE.__inmemory_ext_rwarea=0
FREE.__java_pool_size=0
FREE.__large_pool_size=16777216
FREE.__oracle_base='/opt/oracle'#ORACLE_BASE set from environment
FREE.__pga_aggregate_target=536870912
FREE.__sga_target=1610612736
FREE.__shared_io_pool_size=83886080
FREE.__shared_pool_size=503316480
FREE.__streams_pool_size=0
FREE.__unified_pga_pool_size=0
FREE._instance_recovery_bloom_filter_size=1048576
*.compatible='23.6.0'
*.control_files='/opt/oracle/oradata/FREE/control01.ctl','/opt/oracle/oradata/FREE/control02.ctl','/opt/oracle/oradata/FREE/control03.ctl'
*.db_block_size=8192
*.db_name='FREE'
*.db_recovery_file_dest='/opt/oracle/oradata/fra'
*.db_recovery_file_dest_size=4294967296
*.diagnostic_dest='/opt/oracle'
*.dispatchers='(PROTOCOL=TCP) (SERVICE=FREEXDB)'
*.enable_pluggable_database=true
*.fast_start_parallel_rollback='FALSE'
*.local_listener=''
*.nls_language='AMERICAN'
*.nls_territory='AMERICA'
*.open_cursors=300
*.pga_aggregate_target=512m
*.processes=200
*.remote_login_passwordfile='EXCLUSIVE'
*.sga_target=1536m
*.undo_tablespace='UNDOTBS1'
Successfully copied 1.19kB (transferred 3.07kB) to /home/jorge/oracle-database-lab/docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_spfile.ora
Successfully copied 4.42kB (transferred 6.14kB) to /home/jorge/oracle-database-lab/docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_memoria.ora
Copias guardadas en docs/bitacora/lab6/evidencia/config/
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== VERIFICACIÓN DE db_files ====="

docker exec -i "$CONT_NAME" sqlplus -s -L / as sysdba <<'SQL'
SET LINESIZE 120

SELECT name, value, isspecified
FROM v$spparameter
WHERE name = 'db_files'
  AND sid = '*';

SELECT name, value
FROM v$parameter
WHERE name = 'db_files';

EXIT
SQL
===== VERIFICACIÓN DE db_files =====

NAME
--------------------------------------------------------------------------------
VALUE
------------------------------------------------------------------------------------------------------------------------
ISSPEC
------
db_files

FALSE



NAME
--------------------------------------------------------------------------------
VALUE
------------------------------------------------------------------------------------------------------------------------
db_files
200


jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/02-estados-pdb.sh | tee "$EVID_LAB6/script/$(ts)_02-estados-pdb.script.log"
- **Dónde lo usé:** Parte C.2, modos de apertura de una PDB.
- **Propósito:** Comprobar los estados READ ONLY, RESTRICTED, MOUNTED y READ WRITE.
- **Qué hace (con mis palabras):** Cambié los estados de apertura de FREEPDB1 para ver cómo afectan a los usuarios: READ WRITE permite consultar y modificar, READ ONLY solo consultar, RESTRICTED limita las conexiones a usuarios autorizados y MOUNTED deja la PDB montada sin abrir para trabajo normal. También comprobé que sin SAVE STATE aparece ORA-01109 tras reiniciar, mientras que guardar el estado permite recuperar la apertura automáticamente.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T182735Z_02-estados-pdb.script.log

## Entrada 7 — Parte C.3: validación del arranque

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PARTE C.2: ESTADOS DE FREEPDB1 ====="

set -o pipefail

bash scripts/lab6/02-estados-pdb.sh \
  | tee "$EVID_LAB6/script/$(ts)_02-estados-pdb.script.log"
===== PARTE C.2: ESTADOS DE FREEPDB1 =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:27:35Z origen=02-estados-pdb
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T17:15:07 scn=7554365
== 1. Punto de partida ==

NAME       OPEN_MODE  RES ESTADO_GUARDADO
---------- ---------- --- ----------------------
FREEPDB1   READ WRITE NO  OPEN
== 2. READ ONLY: se puede consultar, no escribir ==

Pluggable database altered.


Pluggable database altered.


Session altered.


ESTUDIANTES
-----------
      20000

1 row selected.

-- Intento de escritura (error esperado: ORA-16000)
UPDATE admin_academia.aca_estudiantes SET estado = estado WHERE estudiante_id = 101
                      *
ERROR at line 1:
ORA-16000: Attempting to modify database or pluggable database that is open for
read-only access.
Help: https://docs.oracle.com/error-help/db/ora-16000/



Session altered.

-- Intento de reabrir en lectura y escritura sin cerrar (error esperado: ORA-65019)
ALTER PLUGGABLE DATABASE freepdb1 OPEN READ WRITE
*
ERROR at line 1:
ORA-65019: pluggable database FREEPDB1 already open
Help: https://docs.oracle.com/error-help/db/ora-65019/


-- FORCE la cierra y la abre en el modo pedido en un solo paso

Pluggable database altered.


NAME       OPEN_MODE  RES ESTADO_GUARDADO
---------- ---------- --- ----------------------
FREEPDB1   READ WRITE NO  OPEN
== 3. RESTRICTED: solo entra quien tiene RESTRICTED SESSION ==

Pluggable database altered.


Pluggable database altered.


NAME       OPEN_MODE  RES ESTADO_GUARDADO
---------- ---------- --- ----------------------
FREEPDB1   READ WRITE YES OPEN
-- C##OPS_RO intenta entrar (error esperado: ORA-01035):
  Error Message = ORA-01035: Login denied. Database is in RESTRICTED mode.

Pluggable database altered.


Pluggable database altered.

-- Reabierta sin restricción:
conectado a FREEPDB1
== 4. Reinicio SIN estado guardado ==

Pluggable database altered.

Database closed.
Database dismounted.
ORACLE instance shut down.
ORACLE instance started.

Total System Global Area 1603398928 bytes
Fixed Size                  5033232 bytes
Variable Size             536870912 bytes
Database Buffers         1056964608 bytes
Redo Buffers                4530176 bytes
Database mounted.
Database opened.

NAME       OPEN_MODE  RES ESTADO_GUARDADO
---------- ---------- --- ----------------------
FREEPDB1   MOUNTED        (sin estado guardado)
-- La aplicación (y C##OPS_RO) intentan entrar por el servicio freepdb1 (error esperado: ORA-01109 u ORA-12514):
  Error Message = ORA-01109: database not open
== 5. Abrir, GUARDAR EL ESTADO y comprobarlo con otro reinicio ==

Pluggable database altered.


Pluggable database altered.

Database closed.
Database dismounted.
ORACLE instance shut down.
ORACLE instance started.

Total System Global Area 1603398928 bytes
Fixed Size                  5033232 bytes
Variable Size             536870912 bytes
Database Buffers         1056964608 bytes
Redo Buffers                4530176 bytes
Database mounted.
Database opened.

NAME       OPEN_MODE  RES ESTADO_GUARDADO
---------- ---------- --- ----------------------
FREEPDB1   READ WRITE NO  OPEN
-- Validación posterior al arranque (C##OPS_RO, solo lectura):
== 0. Por dónde he entrado ==

CONTENEDOR   SERVICIO
------------ ----------------
CDB$ROOT     free
== 1. Instancia y base ==

INSTANCE_N STATUS       LOGINS     ARRANQUE
---------- ------------ ---------- ----------------
FREE       OPEN         ALLOWED    2026-11-24 18:28

NAME             OPEN_MODE            LOG_MODE     DATABASE_ROLE
---------------- -------------------- ------------ ----------------
FREE             READ WRITE           ARCHIVELOG   PRIMARY
== 2. Cada PDB en el modo esperado (y si tiene estado guardado) ==

NAME             OPEN_MODE  RES ESTADO_GUARDADO
---------------- ---------- --- ----------------------
PDB$SEED         READ ONLY  NO  (sin estado guardado)
FREEPDB1         READ WRITE NO  OPEN
== 3. Servicios activos (deben estar los de cada PDB abierta) ==

    CON_ID NAME
---------- ----------------
         1 free
         1 freeXDB
         3 freepdb1
== 4. Errores ORA- en el alert log desde el último arranque, agrupados (compáralos con los de siempre) ==

ERROR      VECES EJEMPLO
--------- ------ -------------------------------------------------------------------------------------
ORA-00800      4 ORA-00800: soft external error, arguments: [Set Priority Failed], [LGWR], [Check trac
ORA-65019      2 ORA-65019 signalled during: ALTER PLUGGABLE DATABASE freepdb1 OPEN READ WRITE...
== 5. Datafiles que no están ONLINE (vacío = bien) ==
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== SALUD DE ORACLE ====="
bash scripts/ops/esperar-healthy.sh

echo "===== VALIDACIÓN DEL ARRANQUE ====="
bash scripts/ops/ro.sh scripts/ops/validar-arranque.sql

echo "===== EVIDENCIA C.2 ====="
ls -lh "$EVID_LAB6/script/"*_02-estados-pdb.script.log
===== SALUD DE ORACLE =====
  t=0s  docker=healthy  cdb/pdb=READWRITE/READWRITE
===== VALIDACIÓN DEL ARRANQUE =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:28:57Z origen=validar-arranque
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7559634
== 0. Por dónde he entrado ==

CONTENEDOR   SERVICIO
------------ ----------------
CDB$ROOT     free
== 1. Instancia y base ==

INSTANCE_N STATUS       LOGINS     ARRANQUE
---------- ------------ ---------- ----------------
FREE       OPEN         ALLOWED    2026-11-24 18:28

NAME             OPEN_MODE            LOG_MODE     DATABASE_ROLE
---------------- -------------------- ------------ ----------------
FREE             READ WRITE           ARCHIVELOG   PRIMARY
== 2. Cada PDB en el modo esperado (y si tiene estado guardado) ==

NAME             OPEN_MODE  RES ESTADO_GUARDADO
---------------- ---------- --- ----------------------
PDB$SEED         READ ONLY  NO  (sin estado guardado)
FREEPDB1         READ WRITE NO  OPEN
== 3. Servicios activos (deben estar los de cada PDB abierta) ==

    CON_ID NAME
---------- ----------------
         1 free
         1 freeXDB
         3 freepdb1
== 4. Errores ORA- en el alert log desde el último arranque, agrupados (compáralos con los de siempre) ==

ERROR      VECES EJEMPLO
--------- ------ -------------------------------------------------------------------------------------
ORA-00800      4 ORA-00800: soft external error, arguments: [Set Priority Failed], [LGWR], [Check trac
ORA-65019      2 ORA-65019 signalled during: ALTER PLUGGABLE DATABASE freepdb1 OPEN READ WRITE...
== 5. Datafiles que no están ONLINE (vacío = bien) ==
===== EVIDENCIA C.2 =====
-rw-r--r-- 1 jorge jorge 4.6K Nov 24 19:28 docs/bitacora/lab6/evidencia/script/20261124T182735Z_02-estados-pdb.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/ro.sh scripts/ops/validar-arranque.sql freepdb1
- **Dónde lo usé:** Parte C.3, validación posterior al reinicio.
- **Propósito:** Comprobar que FREEPDB1 se encuentra abierta y que sus servicios están activos.
- **Qué hace (con mis palabras):** Verifiqué que Oracle quedó operativo tras el reinicio revisando el estado de la instancia, la apertura de FREEPDB1, los servicios de conexión y los archivos necesarios. Sirve para confirmar que no basta con que el contenedor esté encendido: la base y sus servicios también deben estar disponibles para las aplicaciones.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T183104Z_02-validar-pdb.script.log

## Entrada 8 — Parte D.1: servicio academia_app

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== C.3: VALIDACIÓN DESDE FREEPDB1 ====="

bash scripts/ops/ro.sh \
  scripts/ops/validar-arranque.sql \
  freepdb1 \
  | tee "$EVID_LAB6/script/$(ts)_02-validar-pdb.script.log"
===== C.3: VALIDACIÓN DESDE FREEPDB1 =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:31:04Z origen=validar-arranque
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7559728
== 0. Por dónde he entrado ==

CONTENEDOR   SERVICIO
------------ ----------------
FREEPDB1     freepdb1
== 1. Instancia y base ==

INSTANCE_N STATUS       LOGINS     ARRANQUE
---------- ------------ ---------- ----------------
FREE       OPEN         ALLOWED    2026-11-24 18:28

NAME             OPEN_MODE            LOG_MODE     DATABASE_ROLE
---------------- -------------------- ------------ ----------------
FREE             READ WRITE           ARCHIVELOG   PRIMARY
== 2. Cada PDB en el modo esperado (y si tiene estado guardado) ==

NAME             OPEN_MODE  RES ESTADO_GUARDADO
---------------- ---------- --- ----------------------
FREEPDB1         READ WRITE NO  OPEN
== 3. Servicios activos (deben estar los de cada PDB abierta) ==

    CON_ID NAME
---------- ----------------
         3 freepdb1
== 4. Errores ORA- en el alert log desde el último arranque, agrupados (compáralos con los de siempre) ==

ERROR      VECES EJEMPLO
--------- ------ -------------------------------------------------------------------------------------
ORA-65019      1 ORA-65019: pluggable database FREEPDB1 already open
== 5. Datafiles que no están ONLINE (vacío = bien) ==
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PREPARAR EVIDENCIAS 02 ====="

git add \
  docs/bitacora/lab6-ia.md \
  "$EVID_LAB6/script/"*_02-* \
  "$EVID_LAB6/config/"*_02-*

echo "===== ARCHIVOS PREPARADOS ====="
git --no-pager diff --cached --stat

echo "===== ESTADO GIT ====="
git status -sb
===== PREPARAR EVIDENCIAS 02 =====
===== ARCHIVOS PREPARADOS =====
 .../20261124T182539Z_02-init_desde_memoria.ora   | 126 +++++++++++++++
 .../20261124T182539Z_02-init_desde_spfile.ora    |  34 +++++
 .../20261124T182533Z_02-parametros.script.log    |  89 +++++++++++
 .../20261124T182735Z_02-estados-pdb.script.log   | 153 +++++++++++++++++++
 .../20261124T183104Z_02-validar-pdb.script.log   |  32 ++++
 5 files changed, 434 insertions(+)
===== ESTADO GIT =====
## chore/6-administracion-operativa
A  docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_memoria.ora
A  docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_spfile.ora
A  docs/bitacora/lab6/evidencia/script/20261124T182533Z_02-parametros.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T182735Z_02-estados-pdb.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T183104Z_02-validar-pdb.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "feat(ops): parameter safety net, PDB states and post-startup validation" \
  -m "Refs #8"

git status -sb
git log -3 --oneline
[chore/6-administracion-operativa caa5544] feat(ops): parameter safety net, PDB states and post-startup validation
 5 files changed, 434 insertions(+)
 create mode 100644 docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_memoria.ora
 create mode 100644 docs/bitacora/lab6/evidencia/config/20261124T182539Z_02-init_desde_spfile.ora
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T182533Z_02-parametros.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T182735Z_02-estados-pdb.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T183104Z_02-validar-pdb.script.log
## chore/6-administracion-operativa
caa5544 (HEAD -> chore/6-administracion-operativa) feat(ops): parameter safety net, PDB states and post-startup validation
6e6e0eb docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/sysdba.sh scripts/lab6/03-servicio.sql ...
- **Dónde lo usé:** Parte D.1, administración de servicios.
- **Propósito:** Crear y verificar el servicio de conexión de la aplicación Academia.
- **Qué hace (con mis palabras):** Creé y activé el servicio específico academia_app mediante DBMS_SERVICE para que la aplicación se conecte usando su propio nombre de servicio. Después comprobé que figuraba entre los servicios activos y anunciado por el listener, verificando que una base abierta no sirve a la aplicación si su servicio no está disponible.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T183227Z_03-servicio.script.log

## Entrada 9 — Parte D.2: usuario de aplicación

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PARTE D.1: SERVICIO ACADEMIA ====="

bash scripts/ops/sysdba.sh \
  scripts/lab6/03-servicio.sql \
  "$EVID_LAB6/script/$(ts)_03-servicio.script.log"
===== PARTE D.1: SERVICIO ACADEMIA =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:32:27Z origen=03-servicio
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7559784

Session altered.

Servicio academia_app creado
Servicio academia_app arrancado

PL/SQL procedure successfully completed.

== Qué servicios EXISTEN (diccionario de la PDB) ==

NAME             NETWORK_NAME     PDB
---------------- ---------------- ----------
FREEPDB1         FREEPDB1         FREEPDB1
academia_app     academia_app     FREEPDB1

2 rows selected.

== Cuáles están ARRANCADOS ahora (y por tanto se anuncian al listener) ==

NAME                 CON_ID
---------------- ----------
academia_app              3
freepdb1                  3

2 rows selected.

== Que sobreviva a un reinicio: se guarda el estado CON el servicio arrancado ==

Pluggable database altered.

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== SERVICIOS ANUNCIADOS POR ORACLE ====="

docker exec oralab-26ai lsnrctl status \
  | grep -A 2 -E 'Service "(academia_app|freepdb1)"'

echo "===== EVIDENCIA D.1 ====="

ls -lh "$EVID_LAB6/script/"*_03-servicio.script.log
===== SERVICIOS ANUNCIADOS POR ORACLE =====
Service "academia_app" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
Service "freepdb1" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
The command completed successfully
===== EVIDENCIA D.1 =====
-rw-r--r-- 1 jorge jorge 784 Nov 24 19:32 docs/bitacora/lab6/evidencia/script/20261124T183227Z_03-servicio.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Comprobación de APP_ACADEMIA_PWD en config/.env y ejecución de bash scripts/lab6/03-cuenta-app.sh.
- **Dónde lo usé:** Parte D.2, creación de usuarios locales.
- **Propósito:** Configurar la contraseña y crear la cuenta APP_ACADEMIA.
- **Qué hace (con mis palabras):** Configuré la cuenta local APP_ACADEMIA con los permisos necesarios para que la aplicación trabaje, evitando conceder privilegios administrativos innecesarios. La contraseña se almacenó en config/.env (fuera de Git) para separar las cuentas de aplicación de las administrativas y proteger las credenciales.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T183551Z_03-cuenta-app.script.log

## Entrada 10 — Parte D.3: gestión de sesiones

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
nano config/.env
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

bash -c '
source config/.env

for variable in APP_ACADEMIA_PWD ANA_GARCIA_PWD; do
  if [ -n "${!variable:-}" ]; then
    echo "$variable: CONFIGURADA"
  else
    echo "$variable: FALTA"
  fi
done
'
APP_ACADEMIA_PWD: CONFIGURADA
ANA_GARCIA_PWD: CONFIGURADA
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ mkdir -p /tmp/oracle-lab6-fallidos

mv docs/bitacora/lab6/evidencia/script/20261124T183306Z_03-cuenta-app.script.log \
   /tmp/oracle-lab6-fallidos/
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh
set -o pipefail

bash scripts/lab6/03-cuenta-app.sh 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_03-cuenta-app.script.log"
== EVIDENCIA alumno=E047 hora=2026-11-24T18:35:52Z origen=03-cuenta-app
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7560061
== En la raíz: ¿qué prefijo exige Oracle a los usuarios comunes? ==

NAME                 VALUE
-------------------- ------------
common_user_prefix   C##

1 row selected.


Session altered.


PL/SQL procedure successfully completed.


Grant succeeded.


Grant succeeded.

== La cuenta es LOCAL (COMMON = NO): solo existe en FREEPDB1 ==

USERNAME       COMMON ACCOUNT_STATUS   DEFAULT_TABL AUTHENTICATION_TYPE
-------------- ------ ---------------- ------------ -------------------
APP_ACADEMIA   NO     OPEN             USERS        PASSWORD

1 row selected.

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/03-sesiones.sh | tee "$EVID_LAB6/script/$(ts)_03-sesiones.script.log"
- **Dónde lo usé:** Parte D.3, observación y finalización de sesiones.
- **Propósito:** Identificar una sesión con una transacción abierta y comprobar el funcionamiento de CANCEL SQL y KILL SESSION.
- **Qué hace (con mis palabras):** Identifiqué una sesión activa y su proceso para comparar dos formas de intervención: CANCEL SQL cancela únicamente la sentencia en ejecución pero puede dejar la transacción abierta, mientras que KILL SESSION finaliza la sesión completa y provoca el ROLLBACK de los cambios pendientes. Así comprobé que conviene revisar qué está haciendo una sesión antes de cerrarla.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T183652Z_03-sesiones.script.log

## Entrada 11 — Parte E.1: tres perspectivas del diccionario

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PREPARAR PARTE D ====="

git add \
  docs/bitacora/lab6-ia.md \
  "$EVID_LAB6/script/"*_03-*

echo "===== CAMBIOS PREPARADOS ====="

git --no-pager diff --cached --stat

echo "===== VALIDACIÓN ====="

python3 - <<'PY'
import sys
sys.path.insert(0, "scripts/ops")
from autoria import analizar_ia

r = analizar_ia(".", "docs/bitacora/lab6-ia.md")
print("Primera línea obligatoria:", "OK" if r["leido"] else "FALTA")
print("Entradas detectadas:", len(r["entradas"]))
for e in r["entradas"]:
    print("Entrada", e["n"], "COMPLETA" if not e["vacios"] else "INCOMPLETA")
print("Estructura:", "VÁLIDA" if r["leido"] and not r["d1"] and not r["incompletas"] else "REVISAR")
PY
===== PREPARAR PARTE D =====
===== CAMBIOS PREPARADOS =====
 docs/bitacora/lab6-ia.md                         |   5 +-
 .../20261124T183227Z_03-servicio.script.log      |  32 ++++++
 .../20261124T183551Z_03-cuenta-app.script.log    |  30 +++++
 .../20261124T183652Z_03-sesiones.script.log      | 111 +++++++++++++++++++
 4 files changed, 177 insertions(+), 1 deletion(-)
===== VALIDACIÓN =====
Primera línea obligatoria: OK
Entradas detectadas: 1
Entrada 1 COMPLETA
Estructura: VÁLIDA
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "feat(db): add academia_app service and application account; session handling" \
  -m "Refs #8"

echo "===== ESTADO FINAL ====="
git status -sb

echo "===== HISTORIAL ====="
git log -4 --oneline
[chore/6-administracion-operativa 6eeeb9a] feat(db): add academia_app service and application account; session handling
 4 files changed, 177 insertions(+), 1 deletion(-)
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T183227Z_03-servicio.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T183551Z_03-cuenta-app.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T183652Z_03-sesiones.script.log
===== ESTADO FINAL =====
## chore/6-administracion-operativa
===== HISTORIAL =====
6eeeb9a (HEAD -> chore/6-administracion-operativa) feat(db): add academia_app service and application account; session handling
caa5544 feat(ops): parameter safety net, PDB states and post-startup validation
6e6e0eb docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/04-tres-miradas.sh
- **Dónde lo usé:** Parte E.1, visibilidad del diccionario de Oracle.
- **Propósito:** Comparar la información accesible para diferentes usuarios y contenedores.
- **Qué hace (con mis palabras):** Ejecuté consultas equivalentes con distintos usuarios y contenedores para comprobar que la visibilidad depende tanto de los permisos como del contenedor actual: USER_ muestra los objetos propios, ALL_ los accesibles, DBA_ la información administrativa y CDB_ la información de los distintos contenedores.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log

## Entrada 12 — Parte E.2: vistas del diccionario

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== PARTE E.1: TRES MIRADAS AL DICCIONARIO ====="

bash scripts/lab6/04-tres-miradas.sh 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_04-tres-miradas.script.log"
===== PARTE E.1: TRES MIRADAS AL DICCIONARIO =====
== EVIDENCIA alumno=E047 hora=2026-11-24T18:58:27Z origen=04-tres-miradas
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7563581
################ Mirada 1 · C##OPS_RO en CDB$ROOT (con CONTAINER_DATA = ALL) ################

USUARIO        CONTENEDOR
-------------- ----------
C##OPS_RO      CDB$ROOT

VISTA                               FILAS
------------------------------ ----------
USER_TABLES (lo mío)                    0
ALL_TABLES de ADMIN_ACADEMIA            0
ALL_USERS (los que veo)                37
-- DBA_USERS (todo el contenedor actual):

 DBA_USERS
----------
        37
-- CDB_USERS por contenedor (todos los contenedores que tengo permitido ver):

    CON_ID  CDB_USERS
---------- ----------
         1         37
         3         47
-- V$DATAFILE (datafiles visibles):

 DATAFILES
----------
        17
################ Mirada 2 · C##OPS_RO entrando por el servicio freepdb1 ################

USUARIO        CONTENEDOR
-------------- ----------
C##OPS_RO      FREEPDB1

VISTA                               FILAS
------------------------------ ----------
USER_TABLES (lo mío)                    0
ALL_TABLES de ADMIN_ACADEMIA            0
ALL_USERS (los que veo)                47
-- DBA_USERS (todo el contenedor actual):

 DBA_USERS
----------
        47
-- CDB_USERS por contenedor (todos los contenedores que tengo permitido ver):

    CON_ID  CDB_USERS
---------- ----------
         3         47
-- V$DATAFILE (datafiles visibles):

 DATAFILES
----------
        10
################ Mirada 3 · APP_ACADEMIA por academia_app (cuenta de aplicación, sin catálogo) ################

USUARIO        CONTENEDOR
-------------- ----------
APP_ACADEMIA   FREEPDB1

VISTA                               FILAS
------------------------------ ----------
USER_TABLES (lo mío)                    0
ALL_TABLES de ADMIN_ACADEMIA            1
ALL_USERS (los que veo)                47
-- DBA_USERS (todo el contenedor actual):

Error starting at line : 15 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/04-tres-miradas.sql
In command -
SELECT COUNT(*) AS dba_users FROM dba_users
Error at Command Line : 15 Column : 35 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/04-tres-miradas.sql
Error report -
SQL Error: ORA-00942: table or view "SYS"."DBA_USERS" does not exist
Help: https://docs.oracle.com/error-help/db/ora-00942/
-- CDB_USERS por contenedor (todos los contenedores que tengo permitido ver):

Error starting at line : 17 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/04-tres-miradas.sql
In command -
SELECT con_id, COUNT(*) AS cdb_users FROM cdb_users GROUP BY con_id ORDER BY con_id
Error at Command Line : 17 Column : 43 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/04-tres-miradas.sql
Error report -
SQL Error: ORA-00942: table or view "SYS"."CDB_USERS" does not exist
Help: https://docs.oracle.com/error-help/db/ora-00942/
-- V$DATAFILE (datafiles visibles):

Error starting at line : 19 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/04-tres-miradas.sql
In command -
SELECT COUNT(*) AS datafiles FROM v$datafile
Error at Command Line : 19 Column : 35 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/04-tres-miradas.sql
Error report -
SQL Error: ORA-00942: table or view "SYS"."V_$DATAFILE" does not exist
Help: https://docs.oracle.com/error-help/db/ora-00942/
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIA E.1 ====="

ls -lh "$EVID_LAB6/script/"*_04-tres-miradas.script.log

echo "===== ESTADO GIT ====="
git status -sb
===== EVIDENCIA E.1 =====
-rw-r--r-- 1 jorge jorge 3.4K Nov 24 19:58 docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log
===== ESTADO GIT =====
## chore/6-administracion-operativa
?? docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/ro.sh scripts/lab6/04-diccionario.sql
- **Dónde lo usé:** Parte E.2, exploración del diccionario.
- **Propósito:** Comprender el origen de las vistas dinámicas y localizar información sobre cuotas y permisos.
- **Qué hace (con mis palabras):** Exploré las vistas internas del diccionario de Oracle para conocer su origen y localizar información sobre cuotas y operaciones reanudables: las tablas X$ son estructuras internas, V$ son vistas dinámicas de rendimiento, GV$ son vistas globales útiles con varias instancias y los sinónimos públicos permiten consultarlas con nombres más sencillos.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log

## Entrada 13 — Parte E.3: estadísticas y deltas

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

echo "===== PARTE E.2: DICCIONARIO DE ORACLE ====="

bash scripts/ops/ro.sh scripts/lab6/04-diccionario.sql
===== PARTE E.2: DICCIONARIO DE ORACLE =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:01:42Z origen=04-diccionario
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7564671
== EVIDENCIA alumno=E047 hora=2026-11-24T19:01:47Z origen=04-diccionario
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7564680
== 1. Las tablas fijas X$ y las vistas V$ y GV$ que se apoyan en ellas (exponen estructuras de memoria de la instancia y datos del control file) ==

     TOTAL   X_TABLAS   V_VISTAS  GV_VISTAS
---------- ---------- ---------- ----------
      3394       1591        921        880
== 2. V$INSTANCE es GV$INSTANCE filtrada a ESTA instancia ==

VIEW_DEFINITION
------------------------------------------------------------------------------------------------------------------------
select  INSTANCE_NUMBER, INSTANCE_NAME, HOST_NAME, VERSION, VERSION_LEGACY,VERSION_FULL, STARTUP_TIME, STATUS, PARALLEL,
THREAD#, ARCHIVER, LOG_SWITCH_WAIT, LOGINS, SHUTDOWN_PENDING, DATABASE_STATUS, INSTANCE_ROLE, ACTIVE_STATE, BLOCKED,
CON_ID, INSTANCE_MODE, EDITION, FAMILY, DATABASE_TYPE from GV$INSTANCE where inst_id = USERENV('Instance')

== 3. Lo que escribes (V$SESSION, DBA_USERS) son sinónimos públicos ==

OWNER    SYNONYM_NAME   TABLE_OW TABLE_NAME
-------- -------------- -------- ------------------------------
PUBLIC   DBA_USERS      SYS      DBA_USERS
PUBLIC   V$SESSION      SYS      V_$SESSION
== 4. ¿Qué vista me dice las cuotas? Primera trampa: DICTIONARY solo lista lo concedido a PUBLIC o a ti ==

VISTAS_DBA_EN_DICTIONARY
------------------------
                      16
-- Con SELECT_CATALOG_ROLE se pregunta a los comentarios del catálogo (DBA_TAB_COMMENTS):

TABLE_NAME                     COMMENTS
------------------------------ --------------------------------------------------------------------------------
DBA_RESUMABLE                  Resumable session information in the system
DBA_TS_QUOTAS                  Tablespace quotas for all users
== 5. ¿Y qué columnas tiene? (DBA_COL_COMMENTS; MAX_BYTES = -1 significa ilimitada) ==

COLUMN_NAME      COMMENTS
---------------- --------------------------------------------------------------------------------
BLOCKS           Number of ORACLE blocks charged to the user
BYTES            Number of bytes charged to the user
DROPPED          Whether the tablespace has been dropped
MAX_BLOCKS       User's quota in ORACLE blocks.  NULL if no limit
MAX_BYTES        User's quota in bytes.  NULL if no limit
TABLESPACE_NAME  Tablespace name
USERNAME         User with resource rights on the tablespace
== 6. ¿A qué contenedores puede mirar C##OPS_RO? (CONTAINER_DATA) ==

USERNAME   DEFAULT_ATTR OWNER    OBJECT_NAME  ALL_CONTAINERS
---------- ------------ -------- ------------ --------------
C##OPS_RO  Y                                  Y
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIA E.2 ====="

ls -lh "$EVID_LAB6/spool/"*_04-diccionario.spool.log

echo "===== CABECERA ====="

head -n 3 "$(
  ls -t "$EVID_LAB6/spool/"*_04-diccionario.spool.log |
  head -1
)"
===== EVIDENCIA E.2 =====
-rw-r--r-- 1 jorge jorge 3.3K Nov 24 20:01 docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log
===== CABECERA =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:01:47Z origen=04-diccionario
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7564680
SQL Format Cleared
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/sysdba.sh scripts/lab6/04-deltas.sql ...
- **Dónde lo usé:** Parte E.3, medición del rendimiento.
- **Propósito:** Medir el coste de diez recorridos completos sobre la tabla PEDIDO.
- **Qué hace (con mis palabras):** Medí el coste real de las consultas comparando los contadores antes y después de la ejecución (deltas), ya que los contadores de Oracle son acumulativos. De este modo evalué el consumo específico de lecturas lógicas, DB time y DB CPU de la operación en lugar de leer totales acumulados.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T190230Z_04-deltas.script.log

## Entrada 14 — Parte F.1: almacenamiento y cuotas

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

git add \
  docs/bitacora/lab6-ia.md \
  "$EVID_LAB6/script/"*_04-* \
  "$EVID_LAB6/spool/"*_04-*

echo "===== ARCHIVOS PREPARADOS ====="
git --no-pager diff --cached --stat

echo "===== COMPROBACIÓN ====="
git --no-pager diff --cached --check
===== ARCHIVOS PREPARADOS =====
 .../20261124T185827Z_04-tres-miradas.script.log  | 93 ++++++++++++++++++++
 .../script/20261124T190230Z_04-deltas.script.log | 49 +++++++++++
 .../20261124T190147Z_04-diccionario.spool.log    | 49 +++++++++++
 3 files changed, 191 insertions(+)
===== COMPROBACIÓN =====
docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log:7: trailing whitespace.
+C##OPS_RO      CDB$ROOT
docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log:34: trailing whitespace.
+C##OPS_RO      FREEPDB1
docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log:60: trailing whitespace.
+APP_ACADEMIA   FREEPDB1
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:19: trailing whitespace.
+OWNER    SYNONYM_NAME   TABLE_OW TABLE_NAME
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:21: trailing whitespace.
+PUBLIC   DBA_USERS      SYS      DBA_USERS
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:22: trailing whitespace.
+PUBLIC   V$SESSION      SYS      V_$SESSION
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:30: trailing whitespace.
+TABLE_NAME                     COMMENTS
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:32: trailing whitespace.
+DBA_RESUMABLE                  Resumable session information in the system
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:33: trailing whitespace.
+DBA_TS_QUOTAS                  Tablespace quotas for all users
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:36: trailing whitespace.
+COLUMN_NAME      COMMENTS
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:38: trailing whitespace.
+BLOCKS           Number of ORACLE blocks charged to the user
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:39: trailing whitespace.
+BYTES            Number of bytes charged to the user
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:40: trailing whitespace.
+DROPPED          Whether the tablespace has been dropped
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:41: trailing whitespace.
+MAX_BLOCKS       User's quota in ORACLE blocks.  NULL if no limit
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:42: trailing whitespace.
+MAX_BYTES        User's quota in bytes.  NULL if no limit
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:43: trailing whitespace.
+TABLESPACE_NAME  Tablespace name
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:44: trailing whitespace.
+USERNAME         User with resource rights on the tablespace
docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log:49: trailing whitespace.
+C##OPS_RO  Y                                  Y
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "docs(ops): dictionary perspectives and delta measurement" \
  -m "Refs #8"

git status -sb
git log -5 --oneline
[chore/6-administracion-operativa bfa0012] docs(ops): dictionary perspectives and delta measurement
 3 files changed, 191 insertions(+)
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T185827Z_04-tres-miradas.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T190230Z_04-deltas.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/spool/20261124T190147Z_04-diccionario.spool.log
## chore/6-administracion-operativa
bfa0012 (HEAD -> chore/6-administracion-operativa) docs(ops): dictionary perspectives and delta measurement
6eeeb9a feat(db): add academia_app service and application account; session handling
caa5544 feat(ops): parameter safety net, PDB states and post-startup validation
6e6e0eb docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/sysdba.sh scripts/lab6/05-almacenamiento.sql ...
- **Dónde lo usé:** Parte F.1, configuración del almacenamiento.
- **Propósito:** Crear un tablespace con crecimiento limitado y comprobar los errores por falta de cuota.
- **Qué hace (con mis palabras):** Creé el tablespace TBS_ACADEMIA_HIST con 10 MB iniciales y un máximo de 40 MB, configuré alertas de ocupación al 80 % y 95 % y probé los límites de cuota. Comprobé que el espacio libre del tablespace y la cuota del usuario son independientes: aunque haya espacio disponible, un usuario recibe ORA-01950 o ORA-01536 si no tiene cuota suficiente.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log

## Entrada 15 — Parte F.2: operaciones reanudables

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

docker exec -i "$CONT_NAME" sqlplus -s -L / as sysdba <<'SQL'
SET PAGESIZE 50
ALTER SESSION SET CONTAINER = FREEPDB1;

SELECT username, account_status
FROM dba_users
WHERE username = 'CARGA_HIST';

SELECT tablespace_name
FROM dba_tablespaces
WHERE tablespace_name = 'TBS_ACADEMIA_HIST';

EXIT
SQL

Session altered.


no rows selected


no rows selected

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

echo "===== PARTE F.1: ALMACENAMIENTO Y CUOTAS ====="

bash scripts/ops/sysdba.sh \
  scripts/lab6/05-almacenamiento.sql \
  "$EVID_LAB6/script/$(ts)_05-almacenamiento.script.log"
===== PARTE F.1: ALMACENAMIENTO Y CUOTAS =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:04:23Z origen=05-almacenamiento
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7564785

Session altered.

== 1. Un tablespace nuevo con todas sus decisiones: ruta explícita, tamaño inicial y crecimiento CON TECHO ==
TBS_ACADEMIA_HIST creado

PL/SQL procedure successfully completed.


TABLESPACE_NAME    BIG EXTENT_MAN ALLOCATIO SEGMEN
------------------ --- ---------- --------- ------
TBS_ACADEMIA       YES LOCAL      SYSTEM    AUTO
TBS_ACADEMIA_HIST  YES LOCAL      SYSTEM    AUTO

2 rows selected.

== 2. Medir bien: asignado, libre dentro de lo asignado y máximo alcanzable (no son lo mismo) ==

TABLESPACE_NAME    ASIGNADO_MB   LIBRE_MB     MAX_MB
------------------ ----------- ---------- ----------
TBS_ACADEMIA               100       76.8       1024
TBS_ACADEMIA_HIST           10        3.9         40

2 rows selected.


TABLESPACE_NAME    BLOQUES_USADOS BLOQUES_MAX PCT_SOBRE_MAX
------------------ -------------- ----------- -------------
TBS_ACADEMIA                 2976      131072          2.27
TBS_ACADEMIA_HIST             776        5120         15.16

2 rows selected.

== 3. Los tablespaces no crecen solos: crecen sus segmentos. ¿Quién ocupa TBS_ACADEMIA? ==

SEGMENT_NAME               SEGMENT_TY         MB     BLOCKS    EXTENTS
-------------------------- ---------- ---------- ---------- ----------
ACA_MATRICULAS             TABLE               3        384         18
UQ_ACA_MATRICULA_UNICA     INDEX               3        384         18
ACA_ESTUDIANTES            TABLE               2        256         17
IDX_ACA_MAT_EST            INDEX               2        256         17
SYS_C008673                INDEX               2        256         17
UQ_ACA_EMAIL               INDEX               2        256         17

6 rows selected.

== 4. Un esquema de solo esquema SIN cuota en su tablespace por defecto ==

PL/SQL procedure successfully completed.


Table created.

-- La tabla existe... pero todavía no tiene segmento (creación diferida): no ocupa nada

SEGMENTOS_DE_CARGA_HIST
-----------------------
                      0

1 row selected.

-- Primer INSERT: ahora sí hace falta un segmento, y el dueño no tiene cuota (error esperado: ORA-01950)
INSERT INTO carga_hist.registro (id, relleno) VALUES (1, 'x')
                       *
ERROR at line 1:
ORA-01950: The user CARGA_HIST has insufficient quota on tablespace TBS_ACADEMIA_HIST.
Help: https://docs.oracle.com/error-help/db/ora-01950/


== 5. Cuota de 2 MB: la paga el DUEÑO del segmento, aunque inserte otro (error esperado: ORA-01536) ==

User altered.

INSERT INTO carga_hist.registro (id, relleno) SELECT level, 'x' FROM dual CONNECT BY level <= 5000
                       *
ERROR at line 1:
ORA-01536: space quota exceeded for tablespace 'TBS_ACADEMIA_HIST'
Help: https://docs.oracle.com/error-help/db/ora-01536/



Rollback complete.


USERNAME   TABLESPACE_NAME         BYTES  MAX_BYTES     BLOCKS MAX_BLOCKS
---------- ------------------ ---------- ---------- ---------- ----------
CARGA_HIST TBS_ACADEMIA_HIST     2097152    2097152        256        256

1 row selected.

== 6. Las cuotas no se aplican al tablespace temporal (error esperado: ORA-30041) ==
ALTER USER carga_hist QUOTA 10M ON temp
*
ERROR at line 1:
ORA-30041: Cannot grant quota on the tablespace
Help: https://docs.oracle.com/error-help/db/ora-30041/


== 7. Que avise ANTES de llenarse: umbral de alerta para TBS_ACADEMIA_HIST (en la Parte B salía NONE) ==

PL/SQL procedure successfully completed.


TABLESPACE_NAME    OP           AVISO  CRITICO
------------------ ------------ ------ -------
TBS_ACADEMIA       NONE
TBS_ACADEMIA_HIST  GE           80     95

2 rows selected.

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIA F.1 ====="

ls -lh "$EVID_LAB6/script/"*_05-almacenamiento.script.log
===== EVIDENCIA F.1 =====
-rw-r--r-- 1 jorge jorge 3.4K Nov 24 20:04 docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/05-resumable.sh | tee "$EVID_LAB6/script/$(ts)_05-resumable.script.log"
- **Dónde lo usé:** Parte F.2, operaciones RESUMABLE.
- **Propósito:** Comprobar cómo Oracle suspende una carga por falta de cuota y la reanuda después de ampliar el espacio permitido.
- **Qué hace (con mis palabras):** Lancé una inserción de 20.000 registros con cuota insuficiente para el propietario de la tabla. En lugar de abortar con error, Oracle dejó la operación en estado SUSPENDED y, al ampliar la cuota de 2 MB a 30 MB dentro del tiempo permitido, la carga se reanudó automáticamente sin tener que repetirla desde cero.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T190520Z_05-resumable.script.log

## Entrada 16 — Parte F.3: HWM y SHRINK SPACE

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== PARTE F.2: ASIGNACIÓN REANUDABLE ====="

bash scripts/lab6/05-resumable.sh 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_05-resumable.script.log"
===== PARTE F.2: ASIGNACIÓN REANUDABLE =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:05:21Z origen=05-resumable
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7565334
== 0. Permisos TEMPORALES para la prueba (deuda de acceso que se paga en la Parte G) y cuota de partida de 2 MB ==

Session altered.


Grant succeeded.


Grant succeeded.


User altered.

== 1. La aplicación lanza la carga con RESUMABLE (espera hasta 180 s si le falta espacio) ==
== 2. El DBA (12 s después): la sentencia no ha fallado, está SUSPENDIDA ==

NAME             STATUS        TIMEOUT SUSPEND_TIME         ERROR_MSG
---------------- ---------- ---------- -------------------- ----------------------------------------------------------------------
carga-historico  SUSPENDED         180 11/24/26 19:05:20    ORA-01536: space quota exceeded for tablespace 'TBS_ACADEMIA_HIST'

       SID USERNAME      EVENT                                            SECONDS_IN_WAIT
---------- ------------- ------------------------------------------------ ---------------
       205 APP_ACADEMIA  statement suspended, wait error to be cleared     0
FREEPDB1(3):statement in resumable session 'carga-historico' was suspended due to
== 3. Menor cambio útil: ampliar la CUOTA del dueño (no el tablespace, que tiene sitio de sobra) ==

Session altered.


User altered.

-- Lo que vio la aplicación: la carga terminó, con una pausa en medio --

Session altered.


INICIO
--------
19:05:21

1 row selected.


20000 rows created.


Commit complete.


FIN
--------
19:05:34

1 row selected.

FREEPDB1(3):statement in resumable session 'carga-historico' was suspended due to
FREEPDB1(3):statement in resumable session 'carga-historico' was resumed
== 4. Validación: filas cargadas y cuota consumida ==

     FILAS
----------
     20000

USERNAME   TABLESPACE_NAME      USADO_MB   CUOTA_MB
---------- ------------------ ---------- ----------
CARGA_HIST TBS_ACADEMIA_HIST          23         30
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIAS F.1 Y F.2 ====="

ls -lh "$EVID_LAB6/script/"*_05-*
===== EVIDENCIAS F.1 Y F.2 =====
-rw-r--r-- 1 jorge jorge 3.4K Nov 24 20:04 docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log
-rw-r--r-- 1 jorge jorge 1.9K Nov 24 20:05 docs/bitacora/lab6/evidencia/script/20261124T190520Z_05-resumable.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/ops/sysdba.sh scripts/lab6/05-hwm-shrink.sql ...
- **Dónde lo usé:** Parte F.3, recuperación de espacio.
- **Propósito:** Comprobar qué ocurre con el almacenamiento después de eliminar registros y compactar una tabla.
- **Qué hace (con mis palabras):** Inserté 20.000 filas, borré la mayoría hasta dejar 2.000 y comprobé que DELETE no libera automáticamente el espacio asignado porque el segmento mantiene la marca de agua alta (HWM). Al habilitar ROW MOVEMENT y ejecutar SHRINK SPACE, compacté la tabla y reduje el tamaño del segmento aproximadamente de 23 MB a 2,4 MB.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T190646Z_05-hwm-shrink.script.log

## Entrada 17 — Parte G.1: perfiles y gobierno del acceso

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** $ nano docs/bitacora/lab6-ia.md


jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

git add \
  docs/bitacora/lab6-ia.md \
  "$EVID_LAB6/script/"*_05-*

echo "===== ARCHIVOS PREPARADOS ====="
git --no-pager diff --cached --stat

echo "===== ESTADO ====="
git status -sb
===== ARCHIVOS PREPARADOS =====
 docs/bitacora/lab6-ia.md                         | 156 ++++++++++++++++++-
 ...20261124T190423Z_05-almacenamiento.script.log | 112 +++++++++++++
 .../20261124T190520Z_05-resumable.script.log     |  68 ++++++++
 .../20261124T190646Z_05-hwm-shrink.script.log    |  49 ++++++
 4 files changed, 382 insertions(+), 3 deletions(-)
===== ESTADO =====
## chore/6-administracion-operativa
M  docs/bitacora/lab6-ia.md
A  docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T190520Z_05-resumable.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T190646Z_05-hwm-shrink.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "feat(db): tablespace quotas, resumable allocation and space shrink" \
  -m "Refs #8"

echo "===== ESTADO FINAL ====="
git status -sb

echo "===== HISTORIAL ====="
git log -6 --oneline
[chore/6-administracion-operativa 460e2ce] feat(db): tablespace quotas, resumable allocation and space shrink
 4 files changed, 382 insertions(+), 3 deletions(-)
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T190423Z_05-almacenamiento.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T190520Z_05-resumable.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T190646Z_05-hwm-shrink.script.log
===== ESTADO FINAL =====
## chore/6-administracion-operativa
===== HISTORIAL =====
460e2ce (HEAD -> chore/6-administracion-operativa) feat(db): tablespace quotas, resumable allocation and space shrink
bfa0012 docs(ops): dictionary perspectives and delta measurement
6eeeb9a feat(db): add academia_app service and application account; session handling
caa5544 feat(ops): parameter safety net, PDB states and post-startup validation
6e6e0eb docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Comandos para ejecutar y comprobar los scripts de gobierno del acceso de la Parte G.
- **Dónde lo usé:** Parte G.1, perfiles de seguridad, roles y cuentas de usuario.
- **Propósito:** Comprobar la creación de PRF_PERSONAS, los roles funcionales y la cuenta ANA_GARCIA.
- **Qué hace (con mis palabras):** Creé el perfil de seguridad PRF_PERSONAS (que restringe intentos fallidos, tiempos de bloqueo y vigencia de contraseñas), los roles funcionales para agrupar permisos según tareas y la cuenta personal ANA_GARCIA, aplicando así el principio de conceder solo los permisos necesarios para cada función.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log

## Entrada 18 — Parte G.2: pruebas de permisos

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** $ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

docker exec -i "$CONT_NAME" sqlplus -s -L / as sysdba <<'SQL'
SET PAGESIZE 50
ALTER SESSION SET CONTAINER = FREEPDB1;

SELECT username, account_status
FROM dba_users
WHERE username IN ('ANA_GARCIA', 'APP_ACADEMIA');

EXIT
SQL

Session altered.


USERNAME
--------------------------------------------------------------------------------
ACCOUNT_STATUS
--------------------------------
APP_ACADEMIA
OPEN


jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== PARTE G.1: GOBIERNO DEL ACCESO ====="

bash scripts/lab6/06-gobierno-acceso.sh 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_06-gobierno-acceso.script.log"
===== PARTE G.1: GOBIERNO DEL ACCESO =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:33:16Z origen=06-gobierno-acceso
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7571608

Session altered.

== 1. No supongas los valores por defecto: consúltalos (perfil DEFAULT, parámetros de contraseña) ==

RESOURCE_NAME              LIMIT
-------------------------- --------------------------
FAILED_LOGIN_ATTEMPTS      10
INACTIVE_ACCOUNT_TIME      365
PASSWORD_GRACE_TIME        7
PASSWORD_LIFE_TIME         180
PASSWORD_LOCK_TIME         1
PASSWORD_REUSE_MAX         UNLIMITED
PASSWORD_REUSE_TIME        UNLIMITED
PASSWORD_ROLLOVER_TIME     0
PASSWORD_VERIFY_FUNCTION   NULL

9 rows selected.

== 2. Un perfil para PERSONAS (bloqueo de 1 minuto: solo en laboratorio) ==
Perfil PRF_PERSONAS creado

PL/SQL procedure successfully completed.

-- La función de verificación rechaza una contraseña débil (error esperado: ORA-28003)
CREATE USER prueba_debil IDENTIFIED BY "corta" PROFILE prf_personas
*
ERROR at line 1:
ORA-28003: The password chosen did not meet the required complexity rules set by your organization.
ORA-20000: password length less than 8 characters
Help: https://docs.oracle.com/error-help/db/ora-28003/


== 3. Roles FUNCIONALES: lo que se da por rol se administra; lo que se da disperso se persigue ==

PL/SQL procedure successfully completed.


Grant succeeded.


Grant succeeded.


Grant succeeded.


Grant succeeded.

== 4. Alta (joiner): una cuenta NOMINAL para una persona de secretaría ==

PL/SQL procedure successfully completed.


Grant succeeded.

== 5. Pagar la deuda de acceso: APP_ACADEMIA pasa de privilegios sueltos a UN rol ==

PL/SQL procedure successfully completed.


Grant succeeded.

== 6. Resultado: quién tiene qué (roles, privilegios de objeto, de esquema y de sistema) ==

GRANTEE                  GRANTED_ROLE             DEFAULT
------------------------ ------------------------ -------
ANA_GARCIA               ROL_SECRETARIA_ACADEMIA  YES
APP_ACADEMIA             ROL_APP_ACADEMIA         YES
ROL_SECRETARIA_ACADEMIA  ROL_LECTURA_ACADEMIA     YES

3 rows selected.


GRANTEE                  PRIVILEGE          SCHEMA
------------------------ ------------------ ---------------
ROL_LECTURA_ACADEMIA     SELECT ANY TABLE   ADMIN_ACADEMIA

1 row selected.


GRANTEE                  TABLE_NAME       PRIVILEGE
------------------------ ---------------- ------------------
ROL_APP_ACADEMIA         ACA_ESTUDIANTES  SELECT
ROL_APP_ACADEMIA         ACA_ESTUDIANTES  UPDATE

2 rows selected.


GRANTEE                  TABLE_NAME       COLUMN_N PRIVILEGE
------------------------ ---------------- -------- ------------------
ROL_SECRETARIA_ACADEMIA  ACA_ESTUDIANTES  ESTADO   UPDATE

1 row selected.


GRANTEE                  PRIVILEGE
------------------------ ------------------
ANA_GARCIA               CREATE SESSION
APP_ACADEMIA             CREATE SESSION

2 rows selected.


USERNAME      PROFILE       ACCOUNT_STATUS   AUTHENTICATION_TYPE
------------- ------------- ---------------- -------------------
ANA_GARCIA    PRF_PERSONAS  OPEN             PASSWORD
APP_ACADEMIA  DEFAULT       OPEN             PASSWORD

2 rows selected.

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIA G.1 ====="

ls -lh "$EVID_LAB6/script/"*_06-gobierno-acceso.script.log
===== EVIDENCIA G.1 =====
-rw-r--r-- 1 jorge jorge 2.9K Nov 24 20:33 docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Indicaciones para ejecutar y revisar las pruebas de acceso de la Parte G.
- **Dónde lo usé:** Parte G.2, validación de privilegios.
- **Propósito:** Comprobar que los usuarios podían realizar únicamente las operaciones autorizadas.
- **Qué hace (con mis palabras):** Probé tanto operaciones permitidas como prohibidas para validar los roles: comprobé que ANA_GARCIA podía consultar matrículas y modificar el ESTADO de un estudiante, pero no cambiar su nombre. Los errores ORA-41900 y ORA-00942 confirmaron que las restricciones funcionaban según lo esperado.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T193411Z_06-probar-acceso.script.log

## Entrada 19 — Parte G.3: revocación en cascada

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

command -v sql
/home/jorge/oracle/sqlcl/bin/sql
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== PARTE G.2: VALIDAR PERMISOS ====="

bash scripts/lab6/06-probar-acceso.sh 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_06-probar-acceso.script.log"
===== PARTE G.2: VALIDAR PERMISOS =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:34:12Z origen=06-probar-acceso
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7571744
== 1. ANA_GARCIA (persona de secretaría) entra por el servicio freepdb1 ==
-- Roles activos y privilegios de sistema de la sesión

ROLE
--------------------------
ROL_LECTURA_ACADEMIA
ROL_SECRETARIA_ACADEMIA

2 rows selected.


PRIVILEGE
--------------------------
CREATE SESSION

1 row selected.

-- Lee Academia por el privilegio de esquema (también aca_matriculas, que nadie le concedió por nombre)

ESTUDIANTES
-----------
      20000

1 row selected.


MATRICULAS
----------
     60000

1 row selected.

-- Puede cambiar el ESTADO de un estudiante...

1 row updated.


Rollback complete.

-- ...pero no su nombre (error esperado: falta el privilegio UPDATE sobre esa columna)

Error starting at line : 18 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-sesion-ana.sql
In command -
UPDATE admin_academia.aca_estudiantes SET nombres = 'Otro' WHERE estudiante_id = 105
Error at Command Line : 18 Column : 23 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-sesion-ana.sql
Error report -
SQL Error: ORA-41900: missing UPDATE privilege on "ADMIN_ACADEMIA"."ACA_ESTUDIANTES"
Help: https://docs.oracle.com/error-help/db/ora-41900/
-- ...ni borrar (error esperado)

Error starting at line : 20 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-sesion-ana.sql
In command -
DELETE FROM admin_academia.aca_estudiantes WHERE estudiante_id = 105
Error at Command Line : 20 Column : 28 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-sesion-ana.sql
Error report -
SQL Error: ORA-41900: missing DELETE privilege on "ADMIN_ACADEMIA"."ACA_ESTUDIANTES"
Help: https://docs.oracle.com/error-help/db/ora-41900/

Rollback complete.

== 2. APP_ACADEMIA sigue funcionando tras pagar la deuda de acceso ==

ROLE
--------------------
ROL_APP_ACADEMIA

1 row selected.


ESTUDIANTES
-----------
      17600

1 row selected.


1 row updated.


Rollback complete.

-- Ya no puede insertar en el histórico (el permiso temporal de la Parte F se retiró): error esperado

Error starting at line : 12 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-app-sigue.sql
In command -
INSERT INTO carga_hist.registro (id, relleno) VALUES (-1, 'x')
Error at Command Line : 12 Column : 24 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-app-sigue.sql
Error report -
SQL Error: ORA-00942: table or view "CARGA_HIST"."REGISTRO" does not exist
Help: https://docs.oracle.com/error-help/db/ora-00942/
== 3. Tres contraseñas erróneas y después la correcta ==
ORA-01017: invalid credential or not authorized; logon denied
ORA-01017: invalid credential or not authorized; logon denied
ORA-01017: invalid credential or not authorized; logon denied
ORA-28000: The account is locked; login denied.

USERNAME     ACCOUNT_STATUS   LOCK_DATE
------------ ---------------- ------------------
ANA_GARCIA   LOCKED(TIMED)    24-NOV-26
-- El DBA atiende la incidencia (en el mundo real: tras confirmar la identidad de Ana por otro canal)

USERNAME     ACCOUNT_STATUS
------------ ----------------
ANA_GARCIA   OPEN
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIAS DE LA PARTE G ====="

ls -lh "$EVID_LAB6/script/"*_06-*
===== EVIDENCIAS DE LA PARTE G =====
-rw-r--r-- 1 jorge jorge 2.9K Nov 24 20:33 docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log
-rw-r--r-- 1 jorge jorge 3.2K Nov 24 20:34 docs/bitacora/lab6/evidencia/script/20261124T193411Z_06-probar-acceso.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/06-cascada.sh
- **Dónde lo usé:** Parte G.3, administración y revocación de privilegios.
- **Propósito:** Entender las diferencias entre ADMIN OPTION y GRANT OPTION.
- **Qué hace (con mis palabras):** Comprobé qué ocurre al revocar privilegios delegados a terceros: con ADMIN OPTION (privilegios de sistema), revocar al intermediario no hace que sus destinatarios pierdan el privilegio automáticamente; en cambio, con GRANT OPTION (privilegios de objeto), la revocación sí se propaga en cascada a los demás usuarios.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T193525Z_06-cascada.script.log

## Entrada 20 — Parte H.1: objetos inválidos

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh

git add \
  docs/bitacora/lab6-ia.md \
  "$EVID_LAB6/script/"*_06-*

echo "===== ARCHIVOS PREPARADOS ====="
git --no-pager diff --cached --stat

echo "===== ESTADO ====="
git status -sb
===== ARCHIVOS PREPARADOS =====
 ...0261124T193316Z_06-gobierno-acceso.script.log | 113 +++++++++++++++++++
 .../20261124T193411Z_06-probar-acceso.script.log | 106 +++++++++++++++++
 .../20261124T193525Z_06-cascada.script.log       |  78 +++++++++++++
 3 files changed, 297 insertions(+)
===== ESTADO =====
## chore/6-administracion-operativa
A  docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T193411Z_06-probar-acceso.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T193525Z_06-cascada.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ python3 - <<'PY'
import sys
sys.path.insert(0, "scripts/ops")
from autoria import analizar_ia

r = analizar_ia(".", "docs/bitacora/lab6-ia.md")
print("Primera línea:", "OK" if r["leido"] else "FALTA")
print("Entradas:", len(r["entradas"]))
for e in r["entradas"]:
    print("Entrada", e["n"], "COMPLETA" if not e["vacios"] else "INCOMPLETA")
PY
Primera línea: OK
Entradas: 16
Entrada 1 COMPLETA
Entrada 2 COMPLETA
Entrada 3 COMPLETA
Entrada 4 COMPLETA
Entrada 5 COMPLETA
Entrada 6 COMPLETA
Entrada 7 COMPLETA
Entrada 8 COMPLETA
Entrada 9 COMPLETA
Entrada 10 COMPLETA
Entrada 11 COMPLETA
Entrada 12 COMPLETA
Entrada 13 COMPLETA
Entrada 14 COMPLETA
Entrada 15 COMPLETA
Entrada 16 COMPLETA
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "feat(security): person profile, functional roles, nominal account and access debt paid" \
  -m "Refs #8"

echo "===== ESTADO FINAL ====="
git status -sb

echo "===== HISTORIAL ====="
git log -7 --oneline
[chore/6-administracion-operativa fc725ee] feat(security): person profile, functional roles, nominal account and access debt paid
 3 files changed, 297 insertions(+)
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T193316Z_06-gobierno-acceso.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T193411Z_06-probar-acceso.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T193525Z_06-cascada.script.log
===== ESTADO FINAL =====
## chore/6-administracion-operativa
===== HISTORIAL =====
fc725ee (HEAD -> chore/6-administracion-operativa) feat(security): person profile, functional roles, nominal account and access debt paid
460e2ce feat(db): tablespace quotas, resumable allocation and space shrink
bfa0012 docs(ops): dictionary perspectives and delta measurement
6eeeb9a feat(db): add academia_app service and application account; session handling
caa5544 feat(ops): parameter safety net, PDB states and post-startup validation
6e6e0eb docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "feat(security): person profile, functional roles, nominal account and access debt paid" \
  -m "Refs #8"

echo "===== ESTADO FINAL ====="
git status -sb

echo "===== HISTORIAL ====="
git log -7 --oneline
On branch chore/6-administracion-operativa
nothing to commit, working tree clean
===== ESTADO FINAL =====
## chore/6-administracion-operativa
===== HISTORIAL =====
fc725ee (HEAD -> chore/6-administracion-operativa) feat(security): person profile, functional roles, nominal account and access debt paid
460e2ce feat(db): tablespace quotas, resumable allocation and space shrink
bfa0012 docs(ops): dictionary perspectives and delta measurement
6eeeb9a feat(db): add academia_app service and application account; session handling
caa5544 feat(ops): parameter safety net, PDB states and post-startup validation
6e6e0eb docs(ops): add shift checklist and review automated maintenance
be55c4a chore(ops): add Lab 6 kit, AI declaration and starting backup
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Indicaciones de ejecución y comprobación de scripts/lab6/07-objetos.sql.
- **Dónde lo usé:** Parte H.1, dependencias e índices.
- **Propósito:** Comprender la invalidación de vistas y funciones después de cambios en tablas.
- **Qué hace (con mis palabras):** Modifiqué columnas de tablas para ver cómo los cambios estructurales invalidan vistas y funciones dependientes, y cómo recompilarlos. También comprobé qué implica que un índice pase a estado UNUSABLE y cómo recuperarlo mediante su reconstrucción.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T193803Z_07-objetos.script.log

## Entrada 21 — Parte H.2: memoria y advisors

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

docker exec -i "$CONT_NAME" sqlplus -s -L / as sysdba <<'SQL'
SET PAGESIZE 50
ALTER SESSION SET CONTAINER = FREEPDB1;

SELECT object_name, object_type, status
FROM dba_objects
WHERE owner = 'ADMIN_ACADEMIA'
AND object_name IN (
  'ACA_EST_LAB6',
  'V_ACTIVOS_LAB6',
  'V_CONTACTO_LAB6',
  'F_TOTAL_ACTIVOS_LAB6',
  'IX_EST_LAB6_ESTADO'
);

EXIT
SQL

Session altered.


no rows selected

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

echo "===== PARTE H.1: OBJETOS Y DEPENDENCIAS ====="

bash scripts/ops/sysdba.sh \
  scripts/lab6/07-objetos.sql \
  "$EVID_LAB6/script/$(ts)_07-objetos.script.log"
===== PARTE H.1: OBJETOS Y DEPENDENCIAS =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:38:03Z origen=07-objetos
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7572234

Session altered.


PL/SQL procedure successfully completed.

== 1. Montaje: una copia de la tabla, dos vistas y una función que dependen de ella ==

Table created.


Index created.


View created.


View created.


Function created.


OBJECT_NAME          OBJECT_TYP STATUS
-------------------- ---------- -------
F_TOTAL_ACTIVOS_LAB6 FUNCTION   VALID
V_ACTIVOS_LAB6       VIEW       VALID
V_CONTACTO_LAB6      VIEW       VALID
== 2. Columna nueva que nadie usa: Oracle NO invalida nada (dependencia de grano fino) ==

OBJECT_NAME          OBJECT_TYP STATUS
-------------------- ---------- -------
F_TOTAL_ACTIVOS_LAB6 FUNCTION   VALID
V_ACTIVOS_LAB6       VIEW       VALID
V_CONTACTO_LAB6      VIEW       VALID
== 3. Se amplía email_institucional (solo la usa V_CONTACTO_LAB6) ==

OBJECT_NAME          OBJECT_TYP STATUS
-------------------- ---------- -------
F_TOTAL_ACTIVOS_LAB6 FUNCTION   VALID
V_ACTIVOS_LAB6       VIEW       VALID
V_CONTACTO_LAB6      VIEW       INVALID
== 4. Se amplía nombres (la usa V_ACTIVOS_LAB6... y la función, en cascada) ==

OBJECT_NAME          OBJECT_TYP STATUS
-------------------- ---------- -------
F_TOTAL_ACTIVOS_LAB6 FUNCTION   INVALID
V_ACTIVOS_LAB6       VIEW       INVALID
V_CONTACTO_LAB6      VIEW       INVALID
-- La cadena de dependencias que explica la cascada

NAME                   TYPE      REFERENCED_NAME  REFERENCED_TYPE
---------------------- --------- ---------------- ---------------
F_TOTAL_ACTIVOS_LAB6   FUNCTION  V_ACTIVOS_LAB6   VIEW
V_ACTIVOS_LAB6         VIEW      ACA_EST_LAB6     TABLE
V_CONTACTO_LAB6        VIEW      ACA_EST_LAB6     TABLE
== 5. Un usuario llama a la función: Oracle la recompila sola (en SU llamada, en hora punta) ==

   ACTIVOS
----------
     17600

OBJECT_NAME          OBJECT_TYP STATUS
-------------------- ---------- -------
F_TOTAL_ACTIVOS_LAB6 FUNCTION   VALID
V_ACTIVOS_LAB6       VIEW       VALID
V_CONTACTO_LAB6      VIEW       INVALID
== 6. El DBA no espera a que un usuario tropiece: recompila el esquema ANTES de abrir el servicio ==

OBJECT_NAME          OBJECT_TYP STATUS
-------------------- ---------- -------
F_TOTAL_ACTIVOS_LAB6 FUNCTION   VALID
V_ACTIVOS_LAB6       VIEW       VALID
V_CONTACTO_LAB6      VIEW       VALID
== 7. Índices UNUSABLE: un MOVE de la tabla cambia los ROWID y deja el índice inservible, sin dar error ==

INDEX_NAME         STATUS
------------------ --------
IX_EST_LAB6_ESTADO UNUSABLE

INDEX_NAME         STATUS
------------------ --------
IX_EST_LAB6_ESTADO VALID
== 8. Papelera: DROP sin PURGE no libera el espacio ==

ORIGINAL_NAME      OBJECT_NAME_BIN                  TYPE              MB
------------------ -------------------------------- --------- ----------
IX_EST_LAB6_ESTADO BIN$YQvZWoF2LCXgYwIAEazQcg==$0   INDEX             .5
ACA_EST_LAB6       BIN$YQvZWoF3LCXgYwIAEazQcg==$0   TABLE              2

EN_PAPELERA
-----------
          0
== 9. Validación final: inválidos de los esquemas de negocio (debe ser 0) ==

INVALIDOS_NEGOCIO
-----------------
                0
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIA H.1 ====="

ls -lh "$EVID_LAB6/script/"*_07-objetos.script.log
===== EVIDENCIA H.1 =====
-rw-r--r-- 1 jorge jorge 3.0K Nov 24 20:38 docs/bitacora/lab6/evidencia/script/20261124T193803Z_07-objetos.script.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Indicaciones para revisar los resultados de scripts/lab6/07-memoria.sql.
- **Dónde lo usé:** Parte H.2, SGA, PGA y advisors de memoria.
- **Propósito:** Interpretar las recomendaciones de Oracle sobre la memoria de la instancia.
- **Qué hace (con mis palabras):** Analicé la SGA (1.536 MB) y la PGA objetivo (512 MB, con 0 sobreasignaciones) mediante las vistas de los advisors de memoria. Comprobé que duplicar la SGA no aportaba una mejora apreciable en el rendimiento estimado, por lo que no estaba justificado aumentar su tamaño.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T193912Z_07-memoria.script.log

## Entrada 22 — Parte H.3: archivos críticos

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== PARTE H.2: MEMORIA Y ADVISORS ====="

bash scripts/ops/ro.sh scripts/lab6/07-memoria.sql 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_07-memoria.script.log"
===== PARTE H.2: MEMORIA Y ADVISORS =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:39:12Z origen=07-memoria
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7574234
== EVIDENCIA alumno=E047 hora=2026-11-24T19:39:17Z origen=07-memoria
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7574241
== 1. La SGA por componentes (V$SGAINFO) ==

NAME                                       MB RES
---------------------------------- ---------- ---
Maximum SGA Size                         1529 No
Buffer Cache Size                        1008 Yes
Shared Pool Size                          480 Yes
Startup overhead in Shared Pool           223 No
Shared IO Pool Size                        80 Yes
Free SGA Memory Available                  16
Large Pool Size                            16 Yes
Granule Size                               16 No
Fixed SGA Size                              5 No
Redo Buffers                                4 No
Data Transfer Cache Size                    0 Yes
Java Pool Size                              0 Yes
Vector Memory Area Size                     0 No
In-Memory Area Size                         0 No
Streams Pool Size                           0 Yes
== 2. Componentes dinámicos: entre qué tamaños se han movido desde el arranque (ASMM) ==

COMPONENT               ACTUAL_MB     MIN_MB     MAX_MB  FIJADO_MB LAST_OPER_TYP
---------------------- ---------- ---------- ---------- ---------- -------------
DEFAULT buffer cache          928        928        928          0 INITIALIZING
shared pool                   480        480        480          0 STATIC
Shared IO Pool                 80         80         80         80 STATIC
large pool                     16         16         16          0 STATIC

MOVIMIENTOS_GROW_SHRINK
-----------------------
                      0
== 3. La PGA de la instancia (V$PGASTAT) ==

NAME                                    VALOR UNIDAD
---------------------------------- ---------- ------------
aggregate PGA target parameter            512 MB
aggregate PGA auto target                 153 MB
total PGA inuse                           342 MB
total PGA allocated                       403 MB
maximum PGA allocated                     477 MB
over allocation count                       0
cache hit percentage                      100 percent
== 4. Qué procesos consumen más PGA ahora ==

PNAME  SPID                         PGA_MB
------ ------------------------ ----------
M005   6344                           31.6
J000   11156                          14.9
ARC0   6094                           12.8
ARC1   6096                           12.4
ARC2   6098                           12.4
== 5. Antes de cambiar la memoria, pregunta a los advisors (factor 1 = tamaño actual) ==

    SGA_MB     FACTOR ESTD_DB_TIME_FACTOR ESTD_PHYSICAL_READS
---------- ---------- ------------------- -------------------
       768         .5              1.0319               45836
      1152        .75                   1               35947
      1536          1                   1               35947
      1920       1.25                   1               35947
      2304        1.5                   1               35947
      2688       1.75                   1               35947
      3072          2                   1               35947

    PGA_MB     FACTOR    HIT_PCT  OVERALLOC
---------- ---------- ---------- ----------
       128        .25         96          4
       256         .5         96          4
       384        .75        100          0
       512          1        100          0
      1024          2        100          0
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIAS H.2 ====="

ls -lh "$EVID_LAB6/script/"*_07-memoria.script.log

ls -lh "$EVID_LAB6/spool/"*_07-memoria.spool.log
===== EVIDENCIAS H.2 =====
-rw-r--r-- 1 jorge jorge 3.7K Nov 24 20:39 docs/bitacora/lab6/evidencia/script/20261124T193912Z_07-memoria.script.log
-rw-r--r-- 1 jorge jorge 3.6K Nov 24 20:39 docs/bitacora/lab6/evidencia/spool/20261124T193917Z_07-memoria.spool.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Indicaciones para ejecutar y revisar scripts/lab6/07-archivos-criticos.sql.
- **Dónde lo usé:** Parte H.3, inventario y recuperación de la base.
- **Propósito:** Identificar archivos de control, redo logs, SPFILE, archivos archivados y copias RMAN.
- **Qué hace (con mis palabras):** Revisé el inventario de archivos esenciales para el funcionamiento y la recuperación de Oracle: los control files (estructura de la base), los redo logs (cambios para recuperación), los archived logs (secuencias de redo conservadas), las copias gestionadas por RMAN y el uso de la FRA como zona de almacenamiento para recuperación.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T194055Z_07-archivos-criticos.script.log

## Entrada 23 — Parte H.4: ADR y trazas

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab

source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== PARTE H.3: ARCHIVOS CRÍTICOS ====="

bash scripts/ops/ro.sh scripts/lab6/07-archivos-criticos.sql 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_07-archivos-criticos.script.log"
===== PARTE H.3: ARCHIVOS CRÍTICOS =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:40:55Z origen=07-archivos-criticos
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7574293
== EVIDENCIA alumno=E047 hora=2026-11-24T19:41:00Z origen=07-archivos-criticos
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7574304
== 1. Control files (Lab 5, Parte J: tres copias) ==

ARCHIVO              DONDE                                                          STATUS
-------------------- -------------------------------------------------------------- -------
control file         /opt/oracle/oradata/FREE/control01.ctl
control file         /opt/oracle/oradata/FREE/control02.ctl
control file         /opt/oracle/oradata/FREE/control03.ctl
== 2. Redo en línea: grupos y miembros (Lab 5, Parte K: dos miembros por grupo) ==

    GROUP#  SEQUENCE#         MB    MEMBERS STATUS           ARC MEMBER
---------- ---------- ---------- ---------- ---------------- --- --------------------------------------------
         1         25        200          2 INACTIVE         YES /opt/oracle/oradata/FREE/redo01.log
         1         25        200          2 INACTIVE         YES /opt/oracle/oradata/FREE/redo01b.log
         2         26        200          2 CURRENT          NO  /opt/oracle/oradata/FREE/redo02.log
         2         26        200          2 CURRENT          NO  /opt/oracle/oradata/FREE/redo02b.log
         3         24        200          2 INACTIVE         YES /opt/oracle/oradata/FREE/redo03.log
         3         24        200          2 INACTIVE         YES /opt/oracle/oradata/FREE/redo03b.log
== 3. SPFILE, password file y redo archivado ==

ARCHIVO              DONDE
-------------------- --------------------------------------------------------------
spfile               /opt/oracle/product/26ai/dbhomeFree/dbs/spfileFREE.ora
password file        /opt/oracle/product/26ai/dbhomeFree/dbs/orapwFREE
FRA                  /opt/oracle/oradata/fra (138 de 4096 MB)

LOG_MODE     ARCHIVADOS_EN_DISCO
------------ -------------------
ARCHIVELOG                    25
== 4. ¿Hay copia RMAN reciente? (la del simulacro D del Lab 5) ==

ULTIMA_PIEZA_RMA     PIEZAS
---------------- ----------
2026-11-24 19:10          9
== 5. ¿Quién puede conectarse como SYS* por el password file? ==

USERNAME     SYSDB SYSOP SYSBA SYSDG SYSKM ACCOUNT_STATUS
------------ ----- ----- ----- ----- ----- ------------------------------
SYS          TRUE  TRUE  FALSE FALSE FALSE OPEN
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== ARCHIVOS DE CONFIGURACIÓN ORACLE ====="

docker exec "$CONT_NAME" \
  ls -lh /opt/oracle/product/26ai/dbhomeFree/dbs/
===== ARCHIVOS DE CONFIGURACIÓN ORACLE =====
total 2.7G
-rw-r----- 1 oracle oinstall 196M Oct 27 17:21 arch1_10_1237845575.dbf
-rw-r----- 1 oracle oinstall 176M Oct 27 17:21 arch1_11_1237845575.dbf
-rw-r----- 1 oracle oinstall 196M Oct 27 17:26 arch1_12_1237845575.dbf
-rw-r----- 1 oracle oinstall 196M Oct 27 17:32 arch1_13_1237845575.dbf
-rw-r----- 1 oracle oinstall 196M Oct 27 17:32 arch1_14_1237845575.dbf
-rw-r----- 1 oracle oinstall 196M Oct 27 17:32 arch1_15_1237845575.dbf
-rw-r----- 1 oracle oinstall  96M Oct 27 17:44 arch1_16_1237845575.dbf
-rw-r----- 1 oracle oinstall 3.0K Oct 27 17:44 arch1_17_1237845575.dbf
-rw-r----- 1 oracle oinstall  20K Oct 27 17:45 arch1_18_1237845575.dbf
-rw-r----- 1 oracle oinstall  66M Oct  1 13:59 arch1_1_1237845575.dbf
-rw-r----- 1 oracle oinstall  93M Oct 24 12:03 arch1_2_1237845575.dbf
-rw-r----- 1 oracle oinstall 181M Oct 24 13:27 arch1_3_1237845575.dbf
-rw-r----- 1 oracle oinstall 178M Oct 24 19:03 arch1_4_1237845575.dbf
-rw-r----- 1 oracle oinstall 174M Oct 25 12:41 arch1_5_1237845575.dbf
-rw-r----- 1 oracle oinstall 196M Oct 25 17:00 arch1_6_1237845575.dbf
-rw-r----- 1 oracle oinstall  59M Oct 27 17:12 arch1_7_1237845575.dbf
-rw-r----- 1 oracle oinstall 187M Oct 27 17:18 arch1_8_1237845575.dbf
-rw-r----- 1 oracle oinstall 196M Oct 27 17:21 arch1_9_1237845575.dbf
-rw-r----- 1 oracle oinstall  19M Oct  1 14:24 c-1509902213-20261001-00
-rw-r----- 1 oracle oinstall  19M Oct 24 12:42 c-1509902213-20261024-00
-rw-r----- 1 oracle oinstall  19M Oct 24 13:27 c-1509902213-20261024-01
-rw-r----- 1 oracle oinstall  19M Oct 24 13:41 c-1509902213-20261024-02
-rw-r----- 1 oracle oinstall  19M Oct 27 17:25 c-1509902213-20261027-00
-rw-rw---- 1 oracle oinstall 1.6K Nov 24 18:28 hc_FREE.dat
-rw-r----- 1 oracle oinstall 3.1K May 14  2015 init.ora
-rw-r----- 1 oracle oinstall   24 Jul  5 21:57 lkFREE
-rw-r----- 1 oracle oinstall 2.0K Oct 24 12:23 orapwFREE
-rw-r----- 1 oracle oinstall  18M Nov 24 19:10 snapcf_FREE.f
-rw-r----- 1 oracle oinstall 3.5K Nov 24 18:28 spfileFREE.ora
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== EVIDENCIAS H.3 ====="

ls -lh "$EVID_LAB6/script/"*_07-archivos-criticos.script.log

ls -lh "$EVID_LAB6/spool/"*_07-archivos-criticos.spool.log
===== EVIDENCIAS H.3 =====
-rw-r--r-- 1 jorge jorge 2.8K Nov 24 20:41 docs/bitacora/lab6/evidencia/script/20261124T194055Z_07-archivos-criticos.script.log
-rw-r--r-- 1 jorge jorge 2.7K Nov 24 20:41 docs/bitacora/lab6/evidencia/spool/20261124T194100Z_07-archivos-criticos.spool.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Indicaciones para ejecutar y analizar la práctica 07-adr-trazas.
- **Dónde lo usé:** Parte H.4, diagnóstico y trazado de sesiones.
- **Propósito:** Investigar los mensajes del alert log y analizar el coste de una consulta.
- **Qué hace (con mis palabras):** Consulté el repositorio de diagnóstico ADR (donde se centralizan alertas y trazas para investigar errores) y analicé una traza de sesión con TKPROF para medir el coste de una consulta. En la prueba se registraron 249 lecturas lógicas, de las cuales 247 correspondieron a la fase de FETCH.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T194227Z_07-adr-trazas.script.log

## Entrada 24 — Parte I.2: incidente INC-601

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

# Añadir las seis evidencias de la Parte H
git add \
  "$EVID_LAB6/script/"*_07-* \
  "$EVID_LAB6/spool/"*_07-*

# Comprobar que Git las ha preparado
echo "===== ARCHIVOS PREPARADOS ====="
git diff --cached --stat

echo "===== ESTADO ====="
git status -sb
===== ARCHIVOS PREPARADOS =====
 .../20261124T193803Z_07-objetos.script.log       | 100 +++++++++++++++++++
 .../20261124T193912Z_07-memoria.script.log       |  74 ++++++++++++++
 ...61124T194055Z_07-archivos-criticos.script.log |  42 ++++++++
 .../20261124T194227Z_07-adr-trazas.script.log    |  93 +++++++++++++++++
 .../spool/20261124T193917Z_07-memoria.spool.log  |  73 ++++++++++++++
 ...261124T194100Z_07-archivos-criticos.spool.log |  41 ++++++++
 6 files changed, 423 insertions(+)
===== ESTADO =====
## chore/6-administracion-operativa
A  docs/bitacora/lab6/evidencia/script/20261124T193803Z_07-objetos.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T193912Z_07-memoria.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T194055Z_07-archivos-criticos.script.log
A  docs/bitacora/lab6/evidencia/script/20261124T194227Z_07-adr-trazas.script.log
A  docs/bitacora/lab6/evidencia/spool/20261124T193917Z_07-memoria.spool.log
A  docs/bitacora/lab6/evidencia/spool/20261124T194100Z_07-archivos-criticos.spool.log
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ git commit \
  -m "docs(ops): object validity, memory advisors, critical files and ADR tracing" \
  -m "Refs #8"

echo "===== ESTADO FINAL ====="
git status -sb

echo "===== ÚLTIMO COMMIT ====="
git log -1 --oneline
[chore/6-administracion-operativa 3c5fa97] docs(ops): object validity, memory advisors, critical files and ADR tracing
 6 files changed, 423 insertions(+)
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T193803Z_07-objetos.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T193912Z_07-memoria.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T194055Z_07-archivos-criticos.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/script/20261124T194227Z_07-adr-trazas.script.log
 create mode 100644 docs/bitacora/lab6/evidencia/spool/20261124T193917Z_07-memoria.spool.log
 create mode 100644 docs/bitacora/lab6/evidencia/spool/20261124T194100Z_07-archivos-criticos.spool.log
===== ESTADO FINAL =====
## chore/6-administracion-operativa
===== ÚLTIMO COMMIT =====
3c5fa97 (HEAD -> chore/6-administracion-operativa) docs(ops): object validity, memory advisors, critical files and ADR tracing
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Orientaciones para consultar las sesiones bloqueadas y ejecutar ALTER SYSTEM KILL SESSION '206,970' IMMEDIATE; después de comprobar SID y SERIAL#.
- **Dónde lo usé:** Parte I.2, incidente INC-601.
- **Propósito:** Localizar y resolver un bloqueo de transacción.
- **Qué hace (con mis palabras):** Investigué por qué Ana García no podía guardar la ficha del estudiante 101 y descubrí que otra sesión mantenía una transacción bloqueando esa fila. Localicé el SID y SERIAL# de la sesión bloqueadora y la finalicé de forma selectiva en lugar de reiniciar la instancia.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261124T194614Z_08-incidente1-diagnostico.script.log y docs/bitacora/lab6/evidencia/script/20261124T194729Z_08-incidente1-validacion.script.log

## Entrada 25 — Parte I.3: incidente INC-602

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

echo "===== PARTE I: INCIDENTE 1 ====="

bash scripts/lab6/08-guardia.sh incidente 1
===== PARTE I: INCIDENTE 1 =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:45:58Z origen=08-guardia-incidente1
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7574538

+----------------------------------------------------------------------------+
| TICKET INC-601 · prioridad ALTA · 19:46 UTC                                |
| Secretaría (Ana García): «Al guardar la ficha del alumno 101 la pantalla   |
| se queda colgada. Ya he reiniciado mi ordenador dos veces».                |
| Base afectada: FREEPDB1 (Academia).                                        |
+----------------------------------------------------------------------------+

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh
set -o pipefail

echo "===== DIAGNÓSTICO INCIDENTE 1 ====="

bash scripts/ops/ro.sh scripts/lab6/08-diagnostico.sql 2>&1 \
  | tee "$EVID_LAB6/script/$(ts)_08-incidente1-diagnostico.script.log"+
===== DIAGNÓSTICO INCIDENTE 1 =====
== EVIDENCIA alumno=E047 hora=2026-11-24T19:46:15Z origen=08-diagnostico
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-24T18:28:24 scn=7574548
== 1. ¿Quién espera, en qué y por culpa de quién? ==

  SID SERIAL# USERNAME      MODULE      ACTION         EVENT                          WAIT_CLASS    SEG  BLOQ
----- ------- ------------- ----------- -------------- ------------------------------ ----------- ----- -----
   48   29665 ANA_GARCIA    secretaria  ficha-alumno   enq: TX - row lock contention  Application    17   206
  206     970 APP_ACADEMIA  matriculas  cierre-periodo PL/SQL lock timer              Idle           21
== 2. ¿Por qué fila exacta? ==

  SID OBJECT_NAME         ARCHIVO     BLOQUE       FILA
----- ---------------- ---------- ---------- ----------
   48 ACA_ESTUDIANTES        1024        779          5
== 3. Los bloqueos: quién TIENE el TX (lmode 6, block 1) y quién lo PIDE (request 6) ==

  SID TY        ID1        ID2      LMODE    REQUEST      BLOCK
----- -- ---------- ---------- ---------- ---------- ----------
   48 TM      73126          0          3          0          0
   48 TX     327702        804          0          6          0
  206 TM      73126          0          3          0          0
  206 TX     327702        804          6          0          1
== 4. ¿Cuánto trabajo se desharía si se termina al bloqueador? ==

  SID MODULE       USED_UBLK  USED_UREC START_TIME
----- ----------- ---------- ---------- --------------------
  206 matriculas           1          1 11/24/26 19:45:58
== 5. ASH lo guardó segundo a segundo (aunque el bloqueo ya no exista, esto queda) ==

T          SID EVENT                           BLOQ
-------- ----- ------------------------------ -----
19:46:20    48 enq: TX - row lock contention    206
19:46:19    48 enq: TX - row lock contention    206
19:46:18    48 enq: TX - row lock contention    206
19:46:17    48 enq: TX - row lock contention    206
19:46:16    48 enq: TX - row lock contention    206
== 6. Servicios: ¿están arrancados todos los que existen? (NO = existe, pero el listener no lo anuncia) ==

    CON_ID NAME             ARRANCADO
---------- ---------------- ---------
         3 FREEPDB1         SI
         3 academia_app     SI
== 7. Cuentas que no son de Oracle y no están OPEN (LOCKED = a mano; LOCKED(TIMED) = intentos fallidos) ==
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ ls -lh "$EVID_LAB6/script/"*_08-incidente1-diagnostico.script.log
ls: cannot access 'docs/bitacora/lab6/evidencia/script/*_08-incidente1-diagnostico.script.log': No such file or directory
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** bash scripts/lab6/08-guardia.sh incidente 2, ejecución de 08-diagnostico.sql y recuperación del servicio mediante scripts/lab6/03-servicio.sql.
- **Dónde lo usé:** Parte I.3, incidente INC-602.
- **Propósito:** Identificar y corregir un problema de conexión con el servicio academia_app.
- **Qué hace (con mis palabras):** Diagnostiqué un error ORA-12514 con la base de datos abierta: el servicio academia_app existía pero estaba detenido y no aparecía en el listener. Arranqué el servicio y validé que la aplicación volvía a conectarse, comprobando que un error de conexión puede deberse a un servicio concreto y no a una caída de Oracle.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261125T114623Z_08-incidente2-diagnostico.script.log, docs/bitacora/lab6/evidencia/script/20261125T114930Z_08-incidente2-intervencion.script.log y docs/bitacora/lab6/evidencia/script/20261125T114936Z_08-incidente2-validacion.script.log

## Entrada 26 — Parte I.4: incidente INC-603

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ cd ~/oracle-database-lab
source scripts/deployment/env/00-config.sh

echo "===== INTERVENCIÓN INC-602 ====="

bash scripts/ops/sysdba.sh \
  scripts/lab6/03-servicio.sql \
  "$EVID_LAB6/script/$(ts)_08-incidente2-intervencion.script.log"
===== INTERVENCIÓN INC-602 =====
== EVIDENCIA alumno=E047 hora=2026-11-25T11:49:30Z origen=03-servicio
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-25T11:45:10 scn=8578243

Session altered.

Servicio academia_app arrancado

PL/SQL procedure successfully completed.

== Qué servicios EXISTEN (diccionario de la PDB) ==

NAME             NETWORK_NAME     PDB
---------------- ---------------- ----------
FREEPDB1         FREEPDB1         FREEPDB1
academia_app     academia_app     FREEPDB1

2 rows selected.

== Cuáles están ARRANCADOS ahora (y por tanto se anuncian al listener) ==

NAME                 CON_ID
---------------- ----------
academia_app              3
freepdb1                  3

2 rows selected.

== Que sobreviva a un reinicio: se guarda el estado CON el servicio arrancado ==

Pluggable database altered.

jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$ echo "===== VALIDACIÓN INC-602 ====="

{
  echo "== DIAGNÓSTICO POSTERIOR =="
  bash scripts/ops/ro.sh scripts/lab6/08-diagnostico.sql

  echo "== ESTADO DEL LISTENER =="
  docker exec "$CONT_NAME" lsnrctl status

  echo "== PRUEBA DESDE APP_ACADEMIA =="
  bash scripts/ops/app.sh scripts/lab6/06-app-sigue.sql
} 2>&1 | tee "$EVID_LAB6/script/$(ts)_08-incidente2-validacion.script.log"
===== VALIDACIÓN INC-602 =====
== DIAGNÓSTICO POSTERIOR ==
== EVIDENCIA alumno=E047 hora=2026-11-25T11:49:36Z origen=08-diagnostico
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-25T11:45:10 scn=8578359
== 1. ¿Quién espera, en qué y por culpa de quién? ==
== 2. ¿Por qué fila exacta? ==
== 3. Los bloqueos: quién TIENE el TX (lmode 6, block 1) y quién lo PIDE (request 6) ==
== 4. ¿Cuánto trabajo se desharía si se termina al bloqueador? ==
== 5. ASH lo guardó segundo a segundo (aunque el bloqueo ya no exista, esto queda) ==
== 6. Servicios: ¿están arrancados todos los que existen? (NO = existe, pero el listener no lo anuncia) ==

    CON_ID NAME             ARRANCADO
---------- ---------------- ---------
         3 FREEPDB1         SI
         3 academia_app     SI
== 7. Cuentas que no son de Oracle y no están OPEN (LOCKED = a mano; LOCKED(TIMED) = intentos fallidos) ==
== ESTADO DEL LISTENER ==

LSNRCTL for Linux: Version 23.26.3.0.0 - Production on 25-NOV-2026 11:49:40

Copyright (c) 1991, 2026, Oracle.  All rights reserved.

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=0.0.0.0)(PORT=1521)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 23.26.3.0.0 - Production
Start Date                25-NOV-2026 11:45:10
Uptime                    0 days 0 hr. 4 min. 29 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Default Service           FREE
Listener Parameter File   /opt/oracle/product/26ai/dbhomeFree/network/admin/listener.ora
Listener Log File         /opt/oracle/diag/tnslsnr/16351136ca48/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1521)))
Services Summary...
Service "55e54f210f100828e0630b00580adfd0" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
Service "FREE" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
Service "FREEXDB" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
Service "academia_app" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
Service "freepdb1" has 1 instance(s).
  Instance "FREE", status READY, has 1 handler(s) for this service...
The command completed successfully
== PRUEBA DESDE APP_ACADEMIA ==
== EVIDENCIA alumno=E047 hora=2026-11-25T11:49:40Z origen=06-app-sigue
== EVIDENCIA contenedor=16351136ca48 dbid=1509902213 arranque=2026-11-25T11:45:10 scn=8578366

ROLE
--------------------
ROL_APP_ACADEMIA

1 row selected.


ESTUDIANTES
-----------
      17600

1 row selected.


1 row updated.


Rollback complete.

-- Ya no puede insertar en el histórico (el permiso temporal de la Parte F se retiró): error esperado

Error starting at line : 12 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-app-sigue.sql
In command -
INSERT INTO carga_hist.registro (id, relleno) VALUES (-1, 'x')
Error at Command Line : 12 Column : 24 File @ file:/home/jorge/oracle-database-lab/scripts/lab6/06-app-sigue.sql
Error report -
SQL Error: ORA-00942: table or view "CARGA_HIST"."REGISTRO" does not exist
Help: https://docs.oracle.com/error-help/db/ora-00942/
jorge@Jorge ~/oracle-database-lab (chore/6-administracion-operativa)
$
- **Código recibido:** Consulta de DBA_USERS y sentencia ALTER USER app_academia ACCOUNT UNLOCK;.
- **Dónde lo usé:** Parte I.4, incidente INC-603.
- **Propósito:** Identificar el bloqueo administrativo de la cuenta de aplicación y recuperar su acceso.
- **Qué hace (con mis palabras):** Ante el error ORA-28000, comprobé en DBA_USERS que la cuenta APP_ACADEMIA estaba en estado LOCKED (bloqueo administrativo, distinto de LOCKED(TIMED) por intentos fallidos). Desbloqueé únicamente esa cuenta y validé la reconexión de la aplicación, entendiendo por qué hay que proteger estas cuentas frente a procesos automáticos de bajas.
- **Evidencia de ejecución:** docs/bitacora/lab6/evidencia/script/20261125T115039Z_08-incidente3-diagnostico.script.log y docs/bitacora/lab6/evidencia/script/20261125T115132Z_08-incidente3-validacion.script.log

## Entrada 27 — Parte J: preguntas de comprobación

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** Dame las 20 preguntas corregidas con los errores que tengo que añadir
- **Código recibido:** No aplica.
- **Dónde lo usé:** Parte J.2, preparación de lab6-respuestas.md.
- **Propósito:** Recibir una guía con explicaciones y correcciones para las 20 preguntas del laboratorio, interpretar los resultados de las consultas y localizar las evidencias correspondientes.
- **Qué hace (con mis palabras):** Utilicé la guía con las explicaciones de las 20 respuestas que me proporcionó ChatGPT para revisar mis resultados, corregir errores, estructurar las explicaciones y enlazar cada respuesta con su evidencia real en los registros del laboratorio, comprobando que las respuestas técnicas deben justificarse con datos obtenidos en la práctica.
- **Evidencia de ejecución:** No aplica. Documento relacionado: docs/bitacora/lab6-respuestas.md

## Entrada 28 — Parte J: verificación y preparación de la entrega

- **Herramienta:** ChatGPT
- **Prompt (literal, copiado tal cual):** Si ya está bien sigamos que hay que acabar
- **Código recibido:** bash scripts/lab6/09-verificacion-final.sh y comandos de comprobación de Git.
- **Dónde lo usé:** Parte J.1 y J.3, verificación técnica y preparación de la entrega.
- **Propósito:** Detectar requisitos pendientes antes de crear el commit final y el Pull Request.
- **Qué hace (con mis palabras):** Ejecuté 09-verificacion-final.sh para auditar el estado completo de la entrega (base de datos, archivos, evidencias, permisos y documentación). La primera ejecución detectó un fallo porque faltaba lab6-respuestas.md; tras crearlo y repetir la verificación, obtuve RESULTADO: TODO OK. Lab 6 listo para entregar.
- **Evidencia de ejecución:** Primera verificación (1 fallo): docs/bitacora/lab6/evidencia/script/20261125T120617Z_09-verificacion-final.script.log. Segunda verificación (RESULTADO: TODO OK, 25/11/2026, 12:32:14 UTC): docs/bitacora/lab6/evidencia/script/20261125T123214Z_09-verificacion-final.script.log.
