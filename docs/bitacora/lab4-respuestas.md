# Lab 4 — Oracle DBA Workflow I
## 8. Preguntas de comprobación

Respuestas basadas en las pruebas realizadas el 24 de octubre de 2026. Las rutas citadas son relativas a la raíz del repositorio `oracle-database-lab`. Cuando se cita un valor, se indica el resultado observable; las marcas temporales de los nombres son las de los registros generados.

### 8.1.1. Respaldo

**1. ¿Por qué la copia de la Parte B es consistente? ¿Qué pasaría si se tomara con la base abierta?**

Es una **copia en frío**: `backup-estado.sh` ejecuta `SHUTDOWN IMMEDIATE` y detiene el contenedor antes de comprimir el volumen. Así, los datafiles, control files y redo logs se copian en un estado coherente, sin escrituras concurrentes. Si copiáramos directamente los archivos con la base abierta, podrían corresponder a instantes diferentes y la copia no tendría garantizada su recuperación; para un backup en caliente habría que utilizar un procedimiento admitido por Oracle, como RMAN. **Evidencia:** `scripts/ops/backup-estado.sh`, pasos 4 y 5; `docs/bitacora/lab4/evidencia/config/lab4_00-manifiesto-backup.txt` (tipo de copia en frío).

**2. ¿Para qué sirven `manifiesto.txt` y `SHA256SUMS`? ¿Qué comprueba `restaurar-estado.sh` antes de tocar nada?**

`manifiesto.txt` identifica el respaldo y su contexto: etiqueta, fecha UTC, contenedor, volumen, imagen, commit, tipo de copia y número de archivos externos al volumen. `SHA256SUMS` guarda los hashes de los archivos del respaldo para detectar alteraciones o daños. Antes de parar Oracle o sustituir datos, `restaurar-estado.sh` comprueba que Docker responde, localiza la carpeta y ejecuta `sha256sum --check --quiet SHA256SUMS`; si la validación falla, no inicia la restauración. Después exige confirmar el nombre del volumen, salvo que se haya usado `--si`. **Evidencia:** `scripts/ops/backup-estado.sh`, paso 7; `scripts/ops/restaurar-estado.sh`, pasos 1 y 2; `docs/bitacora/lab4/evidencia/script/lab4_00-verificacion-backup.log` (comprobación de integridad satisfactoria).

**3. Define RPO y RTO con los datos de tu propia copia.**

El **RPO** es la pérdida máxima tolerable de información expresada como tiempo. Nuestra copia `backups/20261024T122142Z_lab3-final` conserva el estado del Lab 3 en el punto del respaldo, el 24/10/2026 alrededor de las **12:21 UTC**: si se restaurase esa copia sin otros mecanismos de recuperación, se perderían los cambios posteriores a ese punto. Por tanto, el RPO efectivo ante una recuperación posterior sería el tiempo transcurrido desde esa copia. El **RTO** es el tiempo necesario para volver a prestar servicio tras una incidencia. Aquí incluiría restaurar el volumen, iniciar el contenedor y esperar al estado `healthy`; **todavía no tenemos un RTO medido**, porque comprobamos la integridad de la copia pero no cronometramos una restauración completa. El respaldo ocupaba aproximadamente **521 MB comprimidos** y el volumen alrededor de **4,8 GB**, datos que condicionarán esa medida. **Evidencia:** `docs/bitacora/lab4/evidencia/config/lab4_00-manifiesto-backup.txt`; `docs/bitacora/lab4/evidencia/script/lab4_00-verificacion-backup.log`; `scripts/ops/restaurar-estado.sh`, paso 6. *La cifra de RTO deberá completarse después de un simulacro de restauración.*

### 8.1.2. Diagnóstico y correcciones

**4. ¿Dónde creó Oracle los datafiles de V000 y por qué? ¿Qué parámetro habría evitado el problema?**

Los cinco datafiles de negocio acabaron en `$ORACLE_HOME/dbs`, concretamente bajo `/opt/oracle/product/26ai/dbhomeFree/dbs/`, en lugar de `/opt/oracle/oradata/FREE/FREEPDB1/`. V000 había usado nombres relativos como `academia01.dbf` y `DB_CREATE_FILE_DEST` no estaba configurado; Oracle los resolvió respecto al directorio de trabajo del servidor. Definir `DB_CREATE_FILE_DEST` para Oracle Managed Files (OMF), o emplear rutas absolutas dentro del volumen, habría evitado el problema. **Evidencia:** `docs/bitacora/lab4/evidencia/script/20261024T122615Z_01-diagnostico-inicial.script.log` (rutas fuera del volumen); `scripts/lab4/03-reubicar-datafiles.sh` (destinos corregidos).

**5. ¿Por qué `ALTER TABLESPACE ... RENAME DATAFILE` no basta para mover un archivo?**

Porque esa orden cambia la **ruta registrada por Oracle en el control file**, pero no realiza necesariamente la copia física del archivo al destino. Primero hay que poner el tablespace en un estado seguro, copiar el archivo real manteniendo sus permisos y después actualizar su referencia con `RENAME DATAFILE`; al comprobar que vuelve a estar `ONLINE`, se puede retirar el original. **Evidencia:** `scripts/lab4/03-reubicar-datafiles.sh` (pasos de `OFFLINE`, copia física, `RENAME DATAFILE`, `ONLINE` y eliminación del original); `docs/bitacora/lab4/evidencia/script/20261024T122732Z_03-reubicar-datafiles.script.log`.

**6. ¿Por qué no se edita V000 y se crea V003? ¿Por qué invalidar una contraseña es mejor que borrarla del archivo?**

V000 ya estaba aplicada: modificarla rompería la trazabilidad y haría que instalaciones antiguas y nuevas no compartieran la misma historia de migraciones. Por eso la corrección se expresa como un cambio nuevo, **V003**. Además, borrar una contraseña del archivo actual no la elimina del historial de Git ni la invalida en la base. V003 convirtió las cinco cuentas `ADMIN_*` en **schema-only accounts** (`AUTHENTICATION_TYPE = NONE`), por lo que ya no admiten inicio de sesión mediante la contraseña expuesta. **Evidencia:** `database/migrations/V003__cuentas_esquema_sin_password.sql`; `docs/bitacora/lab4/evidencia/spool/20261024T122936Z_04-V003__cuentas_esquema_sin_password.spool.log`; `scripts/lab4/16-verificacion-final.sh` (`cuentas ADMIN_* con contraseña (0)`).

**7. ¿Qué demuestra la prueba de persistencia y por qué se ejecuta después de reubicar?**

Demuestra que es posible **recrear el contenedor conservando el volumen Docker** y mantener los cinco tablespaces de negocio y sus datos. Se ejecuta después de mover los datafiles porque, si siguieran en la capa efímera del contenedor, se perderían al recrearlo aunque el volumen continuase existiendo. **Evidencia:** `docs/bitacora/lab4/evidencia/script/20261024T123227Z_03-prueba-persistencia.script.log`; `scripts/lab4/16-verificacion-final.sh` (`tablespaces de negocio (5)`, `archivos cuya ruta real sale del volumen (0)`).

### 8.1.3. Instancia y arranque

**8. Con tus evidencias: tres datos que pertenecen a la instancia y tres que pertenecen a la base de datos.**

De la **instancia**: su nombre **FREE**, su estado **OPEN / ACTIVE** y la memoria **Buffer Cache = 1.088 MB** (también sus procesos de fondo, como LGWR). De la **base de datos**: su nombre **FREE**, su `DBID = 1509902213` y su modo de archivado **ARCHIVELOG** (también `OPEN_MODE = READ WRITE` y sus datafiles). Aunque nombre de instancia y base coinciden, representan conceptos distintos: procesos y memoria frente a archivos y datos persistentes. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T133431Z_15-autopsia-instancia.spool.log`, secciones 1 y 2.

**9. ¿Qué lee Oracle en NOMOUNT, en MOUNT y en OPEN? Relaciónalo con ORA-01507 y ORA-01219.**

En **NOMOUNT** Oracle lee la configuración de arranque del SPFILE/PFILE y crea la SGA y los procesos, pero todavía no ha abierto el control file. En **MOUNT** abre los control files e identifica la estructura y los archivos de la base. En **OPEN** abre y comprueba los datafiles y los redo logs necesarios para operar. Por eso en NOMOUNT una consulta que necesita información de la base puede provocar **ORA-01507 (database not mounted)**; y durante MOUNT las consultas a objetos ordinarios pueden dar **ORA-01219**, porque aún no está abierta para consultas generales. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T125351Z_06-arranque-por-etapas.spool.log`; `scripts/lab4/06-arranque-por-etapas.sql`.

**10. ¿Por qué FREEPDB1 se abre sola tras `ALTER DATABASE OPEN`? ¿Qué harías si no lo hiciera?**

Porque quedó guardado su estado de apertura con **`ALTER PLUGGABLE DATABASE FREEPDB1 SAVE STATE`**, de modo que Oracle la reabre al abrir la CDB. Si no lo hiciera, consultaría `V$PDBS`, ejecutaría `ALTER PLUGGABLE DATABASE FREEPDB1 OPEN` desde la raíz y guardaría de nuevo el estado con `SAVE STATE`. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T125351Z_06-arranque-por-etapas.spool.log` (PDB `READ WRITE` tras el arranque); `scripts/lab4/16-verificacion-final.sh` (`FREEPDB1 abierta (READWRITE)`).

**11. Clasifica ORA-00800 y ORA-20013 del alert log: ¿alerta real o ruido conocido? Justifícalo.**

**ORA-00800 [Set Priority Failed]**, observado para procesos como VKTM y LGWR, es un **aviso conocido del contenedor**: Oracle intenta aumentar su prioridad y el entorno no dispone de la capacidad correspondiente (`CAP_SYS_NICE`). No impidió que la base funcionara. **ORA-20013 de DBMS_QOPATCH** también se describe en el enunciado como **ruido conocido** cuando el contenedor no permite leer el inventario de parches. Ninguno justifica por sí solo detener la práctica, pero deben documentarse y comprobarse junto con el estado de la instancia; otros errores ORA- se investigan. En nuestra autopsia sí constan **cuatro registros ORA-00800** en las últimas 24 horas; **no hemos confirmado una aparición de ORA-20013 en los registros aportados**. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T133431Z_15-autopsia-instancia.spool.log`, sección 10; `docs/bitacora/lab4/evidencia/script/20261024T125444Z_06-alert-log.script.log` (revisar los mensajes correspondientes).

### 8.1.4. Parámetros

**12. Diferencia entre `v$parameter` y `v$spparameter` con el ejemplo de `db_files`.**

`V$PARAMETER` muestra el **valor efectivo que utiliza ahora la instancia**; `V$SPPARAMETER` representa lo que está escrito o especificado para el **próximo arranque en el SPFILE**. En el experimento, `db_files` tenía un valor efectivo de **200**. Se pudo fijar **300** solo con `SCOPE=SPFILE`, sin cambiar el valor activo; al ejecutar `ALTER SYSTEM RESET db_files SCOPE=SPFILE`, desapareció ese cambio pendiente. Al final `ISSPECIFIED = FALSE`. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T125730Z_07-parametros-cambios.spool.log`; `scripts/lab4/16-verificacion-final.sh` (`db_files sin línea pendiente en el SPFILE (FALSE)`).

**13. ¿Qué hace `SCOPE=BOTH` y cuál es el `SCOPE` por defecto con SPFILE?**

`SCOPE=BOTH` actualiza el valor **en memoria y en el SPFILE**, por lo que se aplica inmediatamente si el parámetro es dinámico y persiste tras reiniciar. Cuando la instancia utiliza un SPFILE y no se indica `SCOPE`, el comportamiento predeterminado de `ALTER SYSTEM SET` es **BOTH** para los parámetros que admiten ese tipo de cambio. En nuestra prueba, `open_cursors` pasó a **500** con `SCOPE=BOTH` y luego se restauró a **300**. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T125730Z_07-parametros-cambios.spool.log`, sección 2.

**14. ¿Por qué `PROCESSES` rechaza el cambio en memoria aunque `v$parameter` lo marque `IMMEDIATE`?**

Porque **`PROCESSES` es un parámetro de instancia que requiere reinicio** para ajustar sus estructuras internas. La prueba `ALTER SYSTEM SET processes = 250 SCOPE=MEMORY` produjo el error esperado **ORA-02095**. Si se interpreta una columna `IMMEDIATE` en un listado, hay que comprobar que corresponde realmente a `PROCESSES` y no a otro parámetro o capacidad de modificación: en el listado de este laboratorio, `ISSYS_MODIFIABLE` de `PROCESSES` figura como **`FALSE`**, no `IMMEDIATE`. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T125637Z_07-parametros-lectura.spool.log`; `docs/bitacora/lab4/evidencia/spool/20261024T125730Z_07-parametros-cambios.spool.log`, sección 4.

**15. ¿Para qué sirve versionar el PFILE? Explica "configuration drift".**

El PFILE es una representación **legible y comparable** de la configuración; versionarlo permite revisar qué parámetros cambiaron, asociarlos a un commit y recuperar una configuración conocida. *Configuration drift* es la desviación progresiva entre la configuración real y la prevista/versionada, por ejemplo cuando alguien modifica parámetros manualmente y no documenta los cambios. En el laboratorio generamos un PFILE desde SPFILE y otro desde memoria. **Evidencia:** `docs/bitacora/lab4/evidencia/config/initFREE_lab4.ora` (**32 líneas**) y `docs/bitacora/lab4/evidencia/config/initFREE_lab4_memoria.ora` (**122 líneas**); `docs/bitacora/lab4/evidencia/script/20261024T125744Z_07-copiar-pfile.script.log`.

### 8.1.5. Memoria y procesos

**16. ¿Qué modelo de gestión de memoria usa tu instancia? Justifícalo con tres parámetros.**

Utiliza **ASMM (Automatic Shared Memory Management)** para la SGA y gestión automática independiente de la PGA, no AMM unificada. Lo respaldan tres parámetros: `SGA_TARGET = 1536M`, `PGA_AGGREGATE_TARGET = 512M` y `MEMORY_SIZE = 0`. La SGA reparte dinámicamente componentes como Buffer Cache y Shared Pool, mientras la PGA tiene su propio objetivo. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T125640Z_07-parametros-lectura.spool.log`; `docs/bitacora/lab4/evidencia/spool/20261024T133431Z_15-autopsia-instancia.spool.log`, sección 2 (Buffer Cache **1088 MB**, Shared Pool **400 MB**).

**17. Explica las cifras de tu experimento de caché: lecturas lógicas, físicas y tasa de acierto.**

La consulta contó **17.600 estudiantes activos** en ambas rondas. Tras vaciar la caché de Oracle, la **ronda fría** registró **359 lecturas lógicas** y **253 físicas**; al repetir la misma consulta, la **ronda caliente** registró **247 lógicas** y **0 físicas**, porque los bloques ya estaban en el Buffer Cache. Aplicando la fórmula sencilla del ejercicio, `1 − físicas/lógicas`, la tasa de acierto aproximada fue **29,5 %** en frío (`1 − 253/359`) y **100 %** en caliente (`1 − 0/247`). Es una medida de estas rondas, no una tasa global de toda la instancia. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T130150Z_08-experimento-cache.spool.log`.

**18. ¿Por qué no se suma el RSS de los procesos para saber la memoria de la instancia?**

Porque el **RSS** de cada proceso incluye páginas residentes que pueden estar **compartidas**, sobre todo segmentos de la SGA. Al sumar todos los RSS contaríamos muchas veces esas mismas páginas y sobreestimaríamos el consumo. Para evaluar memoria debemos distinguir **SGA compartida**, **PGA privada**, métricas del contenedor y, cuando sea necesario, medidas de memoria proporcional como PSS. **Evidencia:** `docs/bitacora/lab4/evidencia/script/20261024T123918Z_05-instancia-so.script.log` (procesos y uso del contenedor); `docs/bitacora/lab4/evidencia/spool/20261024T133431Z_15-autopsia-instancia.spool.log`, sección 2 (SGA/PGA).

**19. Relaciona el SPID de LGWR de `v$process` con el PID de `/proc`. ¿Por qué `docker top` muestra otro número?**

Oracle mostró para **LGWR `SPID = 2023`** y la exploración de **`/proc` dentro del contenedor** encontró `PID = 2023`, proceso `db_lgwr_FREE`. Son el mismo proceso visto desde Oracle y Linux **dentro del contenedor**. `docker top`, ejecutado desde el anfitrión, puede mostrar otro PID debido a los **espacios de nombres de procesos (PID namespaces)**: el host y el contenedor tienen numeraciones diferentes. No tenemos anotado aquí el PID concreto del host y no conviene inventarlo. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T130516Z_09-procesos.spool.log` (`LGWR 2023`); `docs/bitacora/lab4/evidencia/script/20261024T130520Z_09-procesos-so.script.log` (`2023 ... db_lgwr_FREE`).

**20. ¿Qué hace PMON y qué hace SMON? Pon un ejemplo de cada uno.**

**PMON** supervisa y limpia recursos asociados a procesos o sesiones que terminan anormalmente: por ejemplo, puede detectar un servidor dedicado caído y facilitar la liberación de recursos de esa sesión. **SMON** realiza tareas de mantenimiento y recuperación de instancia: por ejemplo, tras una caída brusca, participa en recuperar el estado consistente de la base usando la información de redo/undo. En nuestra instancia existían ambos procesos, con **PMON PID 1973** y **SMON PID 2029**. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T130516Z_09-procesos.spool.log`; `docs/bitacora/lab4/evidencia/script/20261024T130520Z_09-procesos-so.script.log`.

### 8.1.6. Seguridad y trabajo profesional

**21. ¿Por qué `C##OPS_RO` y no `SYSTEM` para observar? ¿Qué no puede hacer `C##OPS_RO`?**

Por el **principio de mínimo privilegio**: `SYSTEM` es una cuenta administrativa con permisos excesivos para tareas de monitorización, mientras `C##OPS_RO` es un usuario común creado específicamente para leer vistas de diagnóstico. Se le concedió acceso selectivo, incluso `SELECT` sobre `SYS.V_$DIAG_ALERT_EXT`, sin privilegios generales de escritura `ANY`. No puede administrar la base como SYSDBA ni modificar libremente los datos o la configuración; tampoco debe poder escribir en los esquemas de negocio por esos permisos de observabilidad. **Evidencia:** `docs/bitacora/lab4/evidencia/spool/20261024T132358Z_11-ampliar-ops-ro.spool.log` (`V_$DIAG_ALERT_EXT`, `SELECT`, `COMMON=YES`); `scripts/lab4/16-verificacion-final.sh` (`C##OPS_RO sin privilegios ANY de escritura (0)`).

**22. ¿Qué dos vías de exposición de contraseñas corrige este laboratorio respecto al Lab 3?**

La primera era **incluir contraseñas literales en migraciones SQL versionadas**, especialmente V000: aunque se retiren del archivo actual, pueden seguir en el historial Git. Se neutralizó el acceso mediante esas claves convirtiendo las cinco cuentas `ADMIN_*` en cuentas de solo esquema con `NO AUTHENTICATION` mediante V003. La segunda era **pasar la contraseña de SYS en la línea de comandos de los scripts**, donde podría verse en argumentos de procesos, terminales o registros. La versión corregida usa autenticación del sistema operativo como SYSDBA dentro del contenedor (`sqlplus / as sysdba`) y mantiene los secretos locales fuera de Git. **Evidencia:** `database/migrations/V003__cuentas_esquema_sin_password.sql`; `scripts/deployment/env/08-aplicar-migraciones.sh`; `scripts/ops/sysdba.sh`; `scripts/lab4/16-verificacion-final.sh` (`config/.env fuera de Git`, cuentas con contraseña = **0**).
## Preguntas tipo examen P1–P12

**P1. A y D.** Tras SHUTDOWN IMMEDIATE, la copia en frío es consistente y puede restaurarse y abrirse con STARTUP sin recuperación adicional de redo.

**P2. B.** Se pone el tablespace OFFLINE, se copia físicamente el datafile, se actualiza su ruta con RENAME DATAFILE y se vuelve a poner ONLINE.

**P3. A y C.** STARTUP_TIME corresponde al arranque de la instancia; CREATED es la fecha de creación de la base de datos.

**P4. A y C.** En NOMOUNT se pueden consultar parámetros de la instancia y recrear el control file; todavía no está montada la base de datos.

**P5. B.** ALTER DATABASE ARCHIVELOG requiere la base montada, pero no abierta.

**P6. B.** Al arrancar con SPFILE, el SCOPE predeterminado es BOTH para un parámetro dinámico como OPEN_CURSORS: cambia memoria y SPFILE.

**P7. C.** PROCESSES es un parámetro de instancia que no se puede modificar desde una PDB; se produce ORA-65040.

**P8. A y C.** Puede arrancarse con un PFILE válido y después recrear el SPFILE desde ese PFILE corregido.

**P9. B.** MEMORY_TARGET=0 y SGA_TARGET establecido implican ASMM; DB_CACHE_SIZE=512M establece un mínimo para el buffer cache.

**P10. A y D.** La PGA incluye el área de ordenación y, en servidor dedicado, memoria de sesión; shared pool, log buffer y buffer cache pertenecen a la SGA.

**P11. C.** LGWR escribe los registros redo necesarios antes de confirmar normalmente el COMMIT al cliente.

**P12. B y D.** PMON y SMON son procesos esenciales de la instancia; ARC0 y CJQ0 dependen de funciones o configuraciones específicas.
