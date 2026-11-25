# Lab 6 — Respuestas de comprobación

**Alumno:** E047

**Ubicación de las evidencias:** `docs/bitacora/lab6/evidencia/`

## Pregunta 1. Errores ORA- del alert log

**Datos para la respuesta:**

En la Parte B se registraron **6 errores ORA-00800** durante las 24 horas analizadas. Se relacionaban con `Set Priority Failed`, al intentar Oracle modificar prioridades de procesos del sistema operativo dentro de Docker.

El número de errores por sí solo no determina la gravedad: hay que comprobar su causa y si afectan al funcionamiento de la base.

**Evidencia:** `script/20261124T182331Z_01-errores-ora.script.log`.

## Pregunta 2. Ventana de mantenimiento del miércoles

**Datos para la respuesta:**

La ventana de mantenimiento del miércoles comienza a las **22:00**, dura **4 horas** y termina a las **02:00 del jueves**.

Durante las ventanas pueden ejecutarse estas tareas automáticas, que estaban habilitadas:

- `auto optimizer stats collection`: recopilación de estadísticas del optimizador.
- `auto space advisor`: análisis del uso del espacio.
- `sql tuning advisor`: análisis y recomendaciones de optimización SQL.

**Evidencia:** `spool/20261124T182237Z_01-automatizacion.spool.log`.

## Pregunta 3. Diferencias entre V$SPPARAMETER y V$PARAMETER

**Datos para la respuesta:**

El valor inicial de `db_files` en memoria era **200**.

Después de ejecutar:

`ALTER SYSTEM SET db_files=250 SCOPE=SPFILE;`

El SPFILE almacenaba **250**, pero `V$PARAMETER` continuaba mostrando **200**, porque `db_files` es un parámetro estático.

Si no se hubiese revertido el cambio mediante `RESET`, el valor **250** habría entrado en vigor tras reiniciar la instancia.

**Evidencia:** `script/20261124T182533Z_02-parametros.script.log`.

## Pregunta 4. Por qué RESET era correcto para db_files y no para processes

**Datos para la respuesta:**

`db_files` no tenía inicialmente un valor establecido explícitamente en el SPFILE (`ISSPECIFIED=FALSE`). Por eso, `RESET` eliminaba el cambio de prueba y permitía recuperar su valor predeterminado de **200**.

`processes`, en cambio, tenía una configuración explícita de **200**, por lo que aplicar `RESET` eliminaría esa configuración en vez de restaurarla.

**Línea del PFILE que debes comprobar y citar:** `*.processes=200`.

**Evidencias:**

- `config/20261124T182539Z_02-init_desde_spfile.ora`
- `script/20261124T182533Z_02-parametros.script.log`

## Pregunta 5. Error de conexión después del reinicio sin SAVE STATE

**Datos para la respuesta:**

El error real fue:

`ORA-01109: database not open`

La PDB `FREEPDB1` quedó en estado **MOUNTED**, sin estado de apertura guardado.

El mensaje `Database opened` correspondía a la apertura de la instancia y la CDB, pero no garantizaba que `FREEPDB1` estuviera abierta.

**Evidencia:** `script/20261124T182735Z_02-estados-pdb.script.log`, líneas 93–95.

**Corrección:** eliminar la frase de tu documento que decía que aún faltaba averiguar si el error era `ORA-01109` u `ORA-12514`. Ya está confirmado que fue `ORA-01109`.

## Pregunta 6. Identificación de la sesión de aplicación

**Datos de tu documento:**

| Dato | Valor |
|---|---|
| SID | 175 |
| SERIAL# | 57526 |
| SPID | 7015 |
| Evento | `PL/SQL lock timer` |

`USERNAME` identifica la cuenta de Oracle, mientras que `MODULE`, `ACTION` y `CLIENT_IDENTIFIER` permiten conocer mejor qué módulo, operación y usuario funcional originaron la actividad.

El evento `PL/SQL lock timer` correspondía a una espera programada durante la prueba.

**Evidencia:** `script/20261124T183652Z_03-sesiones.script.log`.

## Pregunta 7. Diferencia entre CANCEL SQL y KILL SESSION

**Datos para la respuesta:**

Después de ejecutar `CANCEL SQL`, la aplicación seguía teniendo **1 transacción abierta**.

Esto sucede porque cancelar una sentencia no implica terminar la sesión ni deshacer automáticamente toda la transacción.

Después de `KILL SESSION`, la sesión dejó de mantener esa transacción y se deshicieron sus cambios pendientes.

El estudiante **101** quedó en estado `ACTIVO`.

**Evidencia:** `script/20261124T183652Z_03-sesiones.script.log`.

## Pregunta 8. Valor de common_user_prefix

**Resultado comprobado directamente en Oracle:**

| Parámetro | Valor |
|---|---|
| `common_user_prefix` | `C##` |
| `ISDEFAULT` | `TRUE` |

El prefijo configurado para los usuarios comunes es `C##`, y Oracle está utilizando su valor predeterminado.

Por ejemplo:

- `C##OPS_RO`: cuenta común.
- `APP_ACADEMIA`: cuenta local de `FREEPDB1`.

**Evidencia:** consulta a `V$PARAMETER` realizada el 25/11/2026.

**Corrección:** elimina de esta pregunta los comandos Bash, el error `SELECT: command not found` y las salidas de terminal innecesarias. Incluye únicamente el resultado y su explicación.

## Pregunta 9. Tres perspectivas del diccionario

**Datos de tu documento:**

| Vista | CDB/ROOT con C##OPS_RO | PDB con C##OPS_RO | APP_ACADEMIA |
|---|---|---|---|
| `ALL_TABLES` | 0 | 0 | 1 |
| `DBA_USERS` | 37 | 47 | Sin acceso |
| `CDB_USERS` | CON_ID 1: 37; CON_ID 3: 47 | CON_ID 3: 47 | Sin acceso |
| `V$DATAFILE` | 17 | 10 | Sin acceso |

Las diferencias se deben al contenedor desde el que se consulta y a los privilegios del usuario.

`ALL_TABLES` muestra las tablas accesibles al usuario; las vistas `DBA_` y `CDB_` ofrecen información administrativa que requiere los permisos correspondientes.

**Evidencia:** `script/20261124T185827Z_04-tres-miradas.script.log`.

## Pregunta 10. Lecturas lógicas y DB time

**Datos de tu documento:**

| Métrica | Valor |
|---|---:|
| Lecturas lógicas acumuladas | 54.696 |
| Lecturas aproximadas por recorrido | 5.470 |
| DB time | 0,68 segundos |
| DB CPU | 0,59 segundos |

La diferencia entre DB time y DB CPU fue aproximadamente **0,09 segundos**.

Como ambos valores estaban próximos, la mayor parte del tiempo registrado correspondía a procesamiento de CPU y no a esperas.

**Evidencia:** `script/20261124T190230Z_04-deltas.script.log`.

## Pregunta 11. Espacio de TBS_ACADEMIA_HIST

**Datos de tu documento:**

| Medida | Valor inicial |
|---|---:|
| Asignado | 10 MB |
| Libre | 3,9 MB |
| Máximo | 40 MB |

El espacio asignado es la capacidad actual del datafile, el espacio libre es la parte aún disponible y el máximo es el límite hasta el que puede crecer.

Para anticipar problemas de capacidad, se configuraron umbrales de alerta del **80 %** y del **95 %**.

**Evidencia:** `script/20261124T190423Z_05-almacenamiento.script.log`.

## Pregunta 12. Quién inserta y quién paga la cuota

**Datos para la respuesta:**

El `INSERT` fue ejecutado por **SYS**, pero la tabla pertenecía a **CARGA_HIST**.

La cuota correspondía al propietario del segmento, es decir, `CARGA_HIST`.

`ORA-01950` apareció cuando el propietario no disponía de cuota suficiente. Posteriormente, una cuota de **2 MB** resultó insuficiente y apareció `ORA-01536`.

Ampliar el tamaño del tablespace no solucionaría `ORA-01536`, porque el límite alcanzado era la cuota del usuario.

**Evidencia:** `script/20261124T190423Z_05-almacenamiento.script.log`.

## Pregunta 13. Suspensión de la carga RESUMABLE

**Datos de tu documento:**

La carga reanudable estuvo suspendida aproximadamente **12 segundos**, frente a un tiempo máximo configurado de **180 segundos**.

Oracle registró la suspensión y el error de cuota, y la sentencia se observó en estado `SUSPENDED` mediante `DBA_RESUMABLE`.

Al aumentar la cuota de **2 MB a 30 MB**, la ejecución pudo continuar y completar las **20.000 inserciones**.

**Evidencia:** `script/20261124T190520Z_05-resumable.script.log`.

## Pregunta 14. Comparación antes y después de SHRINK

**Datos de tu documento:**

| Medida | Antes | Después |
|---|---:|---:|
| Filas | 20.000 | 2.000 |
| Bloques | 2.944 | 304 |
| Espacio aproximado del segmento | 23 MB | 2,4 MB |

`DELETE` elimina registros, pero no necesariamente devuelve al tablespace el espacio asignado al segmento.

`SHRINK SPACE` permite compactar el segmento y liberar espacio, siempre que se cumplan sus requisitos, como habilitar `ROW MOVEMENT` en este caso.

**Evidencia:** `script/20261124T190646Z_05-hwm-shrink.script.log`.

## Pregunta 15. DEFAULT y PRF_PERSONAS

**Valores de DEFAULT indicados en tu documento:**

| Parámetro | Valor |
|---|---|
| `FAILED_LOGIN_ATTEMPTS` | 10 |
| `PASSWORD_LOCK_TIME` | 1 día |
| `PASSWORD_LIFE_TIME` | 180 días |
| `PASSWORD_GRACE_TIME` | 7 días |
| `INACTIVE_ACCOUNT_TIME` | 365 días |

Para `PRF_PERSONAS` configuraste:

- **3 intentos fallidos** antes del bloqueo.
- **1 minuto de bloqueo temporal**, elegido para la prueba del laboratorio.
- **90 días de vigencia de contraseña**.
- **7 días de gracia**.
- Verificación de contraseñas mediante `ora12c_verify_function`.

Dos límites que puedes justificar son el máximo de intentos fallidos, para dificultar ataques de contraseña, y el tiempo de bloqueo, que en el laboratorio permite recuperar rápidamente la cuenta.

**Evidencia:** `script/20261124T193316Z_06-gobierno-acceso.script.log`.

## Pregunta 16. Privilegios de Ana García

**Datos para la respuesta:**

Ana tenía asignado `ROL_SECRETARIA_ACADEMIA`, que le proporcionaba los permisos funcionales correspondientes.

La lectura de `ACA_MATRICULAS` era posible gracias a los permisos concedidos mediante roles y el privilegio de lectura sobre el esquema, sin necesidad de un permiso individual sobre esa tabla.

Al intentar modificar el nombre de un estudiante apareció **`ORA-41900`**, porque la actualización estaba limitada a la columna `ESTADO`.

**Evidencias:**

- `script/20261124T193316Z_06-gobierno-acceso.script.log`
- `script/20261124T193411Z_06-probar-acceso.script.log`

## Pregunta 17. Invalidación de objetos

**Datos de tu documento:**

| Modificación | Resultado |
|---|---|
| Añadir `TELEFONO` | No invalidó dependencias |
| Ampliar `EMAIL_INSTITUCIONAL` | Invalidó `V_CONTACTO_LAB6` |
| Ampliar `NOMBRES` | Invalidó `V_ACTIVOS_LAB6` y `F_TOTAL_ACTIVOS_LAB6` |

Añadir una columna nueva no alteraba las dependencias existentes que se estaban comprobando.

Modificar la definición de columnas utilizadas por vistas o funciones sí provocó invalidaciones.

Al terminar la práctica, los objetos de negocio quedaron válidos.

**Evidencia:** `script/20261124T193803Z_07-objetos.script.log`.

## Pregunta 18. Advisors de SGA y PGA

**Datos de tu documento:**

| Métrica | Valor |
|---|---:|
| SGA actual | 1.536 MB |
| SGA duplicada | 3.072 MB |
| Factor estimado con SGA duplicada | 1 |
| PGA objetivo | 512 MB |
| Sobreasignaciones actuales | 0 |
| Sobreasignaciones con PGA de 128/256 MB | 4 |
| Sobreasignaciones desde 384 MB | 0 |

Duplicar la SGA no ofrecía una mejora apreciable del DB time estimado.

En los escenarios analizados, reducir la PGA por debajo de **384 MB** provocaba sobreasignaciones.

Por tanto, los advisors no aportaban una justificación para aumentar la memoria en ese momento.

**Evidencia:** `script/20261124T193912Z_07-memoria.script.log`.

## Pregunta 19. Lecturas lógicas de la consulta trazada

**Datos de tu documento:**

La consulta de estudiantes activos devolvió **17.600 registros**.

TKPROF mostró **249 lecturas lógicas** en total, distribuidas así:

- `PARSE`: 2.
- `FETCH`: 247.

En TKPROF, la columna `query` recoge las lecturas lógicas consistentes. Debes identificar esa columna en el resultado de la consulta trazada.

**Evidencia:** `script/20261124T194227Z_07-adr-trazas.script.log`.

## Pregunta 20. Tres incidentes de guardia

| Incidente | Evidencia clave | Intervención | Validación |
|---|---|---|---|
| **INC-601** | Sesión 48 esperando bloqueo TX de la sesión 206 | `ALTER SYSTEM KILL SESSION '206,970' IMMEDIATE;` | Desaparece el bloqueo y estudiante 101 `ACTIVO` |
| **INC-602** | Servicio `academia_app` marcado como `NO` | `DBMS_SERVICE.START_SERVICE('academia_app')` | Servicio `READY`, aplicación conectada y 17.600 estudiantes consultados |
| **INC-603** | `APP_ACADEMIA` en estado `LOCKED` | `ALTER USER app_academia ACCOUNT UNLOCK;` | Cuenta `OPEN`, aplicación conectada y actualización de prueba con `ROLLBACK` |

**Evidencias:**

- `script/20261124T194614Z_08-incidente1-diagnostico.script.log`
- `script/20261124T194729Z_08-incidente1-validacion.script.log`
- `script/20261125T114623Z_08-incidente2-diagnostico.script.log`
- `script/20261125T114936Z_08-incidente2-validacion.script.log`
- `script/20261125T115039Z_08-incidente3-diagnostico.script.log`
- `script/20261125T115132Z_08-incidente3-validacion.script.log`

Simulacro 1Z0-182 · Las 22 respuestas


Pregunta	Respuesta					Parte

S1		B — MMON					F
S2		C — Sesiones nuevas				C
S3		B — CREATE PFILE FROM MEMORY			C
S4		B y C — Apertura forzada o cerrar y abrir	C
S5		C — DBA_PDB_SAVED_STATES			C
S6		B — ORA-01035					C
S7		A — DBMS_SERVICE				D
S8		B — PADDR = ADDR				D
S9		C — La transacción permanece abierta		D
S10		C — PUBLIC					D
S11		B — V$CON_SYSMETRIC				E
S12		A y C — CPU y esperas no Idle			E
S13		B — HR						F
S14		A y C — Undo y temporal				F
S15		A y C — Suspensión y DBA_RESUMABLE		F
S16		B — Row movement y ASSM				F
S17		B — LOCKED(TIMED)				G
S18		B — Conserva el privilegio			G
S19		A y B — MOVE y UNUSABLE				H
S20		B — DBMS_MONITOR.SESSION_TRACE_ENABLE		H
S21		C — DIAGNOSTIC_DEST				H
S22		C — Identificar al bloqueador			I
