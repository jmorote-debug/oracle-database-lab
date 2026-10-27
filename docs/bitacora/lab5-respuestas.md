# Lab 5 — Oracle DBA Workflow II: índices, rendimiento y durabilidad

## 8. Preguntas de comprobación

Respuestas correspondientes a las pruebas realizadas el **27 de octubre de 2026** en Oracle Free (`FREE` / `FREEPDB1`, contenedor `oralab-26ai`). Las rutas de evidencia son relativas a la raíz de `oracle-database-lab`. Se citan valores de nuestras ejecuciones y no los valores ideales del enunciado.

### 8.1. Punto de partida y banco de medida (A, B)

**1. Compara el paso 6 de tu copia `lab4-final` con el de la copia `lab3-final`. ¿Qué demuestra la diferencia?**

En la copia `lab4-final`, el **paso 6, «Archivos fuera del volumen»**, responde **«ninguno: el volumen contiene toda la base de datos»**. En el estado heredado del Lab 3 se habían detectado datafiles de los tablespaces de negocio fuera de `/opt/oracle/oradata`, bajo el directorio de instalación de Oracle; ese problema se corrigió en el Lab 4. La diferencia demuestra que una copia del volumen ahora incluye los archivos necesarios de la base y que recrear el contenedor no debería perder esos datafiles. El manifiesto también confirma que se incluyen SPFILE y password file. No interpreto esto como prueba de restauración hasta realizarla: esa prueba se hizo después en O.C. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T171313Z_00-backup-lab4.script.log`, paso 6; `docs/bitacora/lab4-respuestas.md`, preguntas 4 y 7; `scripts/lab4/16-verificacion-final.sh` (ningún archivo real fuera del volumen).

**2. Calcula el factor de bloqueo (bfr) de CLIENTE y PEDIDO. ¿Por qué PEDIDO cabe casi el triple de filas por bloque?**

Con las estadísticas que recogimos, **CLIENTE: 100.000 / 1.517 = 65,92 ≈ 66 filas/bloque**; **PEDIDO: 1.000.000 / 5.320 = 187,97 ≈ 188 filas/bloque**. La razón es **188 / 66 ≈ 2,85 veces**. La fila media de CLIENTE ocupa **102 bytes**, frente a **32 bytes** de PEDIDO; con bloques del mismo tamaño, una fila más corta permite almacenar muchas más entradas. Es una media estadística que también está condicionada por cabeceras y espacio interno de los bloques. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T171818Z_01-perfil-tiendasur.script.log`, apartado 1.

**3. ¿Por qué el banco de medida ejecuta cada sentencia dos veces y mide solo la segunda?**

La primera ejecución calienta la caché y puede incluir trabajo puntual de preparación o carga de bloques. La segunda reduce esa variabilidad y permite comparar de forma más estable el plan y, sobre todo, los **Buffers** (lecturas lógicas). No implica que todas las ejecuciones reales vayan a ser así de rápidas ni elimina la necesidad de considerar lecturas físicas. En C, la búsqueda por `ID_PEDIDO = 4711` necesitó **4 buffers** al leer índice más tabla; pidiendo solo `ID_PEDIDO` necesitó **3**. **Evidencia:** `scripts/lab5/01-herramienta-medir.sql`; `docs/bitacora/lab5/evidencia/script/20261027T171927Z_02-anatomia-indice.script.log`, apartado 3.

### 8.1.1. Anatomía y tipos de índice (C, D)

**4. Altura, hojas y fan-out real de `IX_PED_CLIENTE`. ¿Y con mil millones de filas?**

`IX_PED_CLIENTE` tenía **altura 3**, **2.216 hojas**, **6 bloques de rama** y **2.215 entradas de rama**. El fan-out real calculado en el ejercicio es **(2.216 + 6 − 1)/6 ≈ 370**; el fan-out máximo estimado es **543**. Para **1.000 millones de filas**, manteniendo las densidades y tamaños supuestos en la simulación, el índice pasaría a aproximadamente **2.208.969 hojas** y **altura 4**, de modo que una búsqueda con acceso posterior a la tabla costaría aproximadamente **5 lecturas**. Es una proyección, no una carga de mil millones de filas ejecutada. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T171927Z_02-anatomia-indice.script.log`, apartado 2.

**5. Descompón una entrada de `PK_CLIENTE` y su ROWID. ¿Por qué no aparece el número de archivo?**

En el volcado de la primera hoja se ve `row#0 ... data:(6): 00 00 03 1b 00 00`. Los **primeros cuatro bytes** (`00 00 03 1b`, hexadecimal `0x31B`) identifican el **bloque 795**; los **dos últimos** (`00 00`) representan la **ranura 0**. La clave de esa entrada, `c1 02`, corresponde al cliente 1. En esta estructura Oracle usa el **ROWID restringido/corto** de la entrada del índice, sin almacenar explícitamente un número de archivo en esos seis bytes; el contexto físico lo aporta el segmento/tablespace. **Evidencia:** `docs/bitacora/lab5/evidencia/config/20261027T171927Z_02-volcado-indice.trc.txt`; `docs/bitacora/lab5/evidencia/script/20261027T171927Z_02-anatomia-indice.script.log`, apartado 4.

**6. Tres pruebas de la Parte D, con lecturas lógicas.**

- **Único en DNI (Q13):** sin índice, **1.486 buffers** y `TABLE ACCESS FULL`; con `UX_CLI_DNI`, **3 buffers** y `INDEX UNIQUE SCAN`. Además, una inserción de DNI duplicado fue rechazada con `ORA-00001`, por lo que el índice también garantiza integridad.
- **Compuesto/cubriente (Q7):** índice simple por cliente, **15 buffers** y ordenación; índice `(id_cliente, fecha_pedido)`, **7**; índice cubriente, **3**, sin consultar el segmento de tabla. La mejora procede del orden físico por la clave y de que las columnas consultadas ya están en el índice.
- **Bitmap (Q14):** recorrido completo del hecho de ventas, **4.073 buffers**; combinación de cuatro índices bitmap, **528 buffers**. Conviene para una carga analítica de baja concurrencia de escritura, no para modificar masivamente filas OLTP.

**Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T172114Z_03-tipos-indice.script.log`, apartados 1, 3 y 6.

### 8.1.2. Agrupamiento, equilibrio y sargabilidad (E, F)

**7. ¿Por qué `IX_PED_FECHA` tiene CF próximo a bloques y `IX_PED_CLIENTE` próximo a filas? ¿Lo arreglaría REBUILD?**

`IX_PED_FECHA` tiene **CF = 5.220**, próximo a los **5.320 bloques** de PEDIDO: las filas consecutivas por fecha suelen estar próximas físicamente. `IX_PED_CLIENTE` tiene **CF = 999.041**, próximo al **millón de filas**: recorrer clientes en orden obliga a saltar de bloque casi por cada registro. El factor de agrupamiento refleja la **correspondencia entre el orden de las entradas del índice y la colocación física de las filas**. Un `REBUILD` del índice por sí solo no reordena la tabla y, por tanto, no resuelve ese mal agrupamiento. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T172145Z_04-agrupamiento-equilibrio.script.log`, apartados 1 y 2.

**8. Según la curva, ¿cuándo deja de compensar cada índice? Compáralo con la fórmula.**

Para el índice de **CF malo**, la prueba pasa de **975 buffers** con **0,1 %** de filas a **2.004 buffers** con **0,2 %**; el script ya muestra que el optimizador escoge recorrido completo a partir del **0,2 %** en ese escenario. Desde el **1 %**, el índice malo costaría **9.920 buffers**, mucho más que los **5.232** del barrido de tabla. El índice de **CF bueno** sigue por debajo de 5.232 incluso con **50 %** de filas (**3.938 buffers**), pero pierde al recorrer el **100 %** (**7.875 > 5.232**). En la comparación teórica, `1/bfr = 1/188 ≈ 0,53 %` para un índice malo suponiendo igual coste por lectura; si una lectura aleatoria cuesta cinco veces una secuencial, el umbral teórico baja a **0,11 %**. Son aproximaciones de coste; la curva real depende del plan y de los bloques recorridos. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T172145Z_04-agrupamiento-equilibrio.script.log`, apartado 3.

**9. ¿Por qué `LIKE 'Gonz%'` usa índice y aun así lee más que un recorrido completo?**

`'Gonz%'` permite un **rango de claves** en un B-tree, porque el prefijo está fijado; `'%ez'` no permite una búsqueda por el extremo izquierdo. Sin embargo, recuperar las **2.056 filas** que cumplen `Gonz%` desde el índice de apellidos implicó muchas visitas dispersas a bloques de CLIENTE: **2.024 buffers**. El recorrido completo de referencia de CLIENTE era del orden de **1.486 buffers**. Ser sargable permite considerar el índice, pero **no garantiza que sea más barato**: también importa el clustering factor y cuántas filas y columnas se recuperan. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T172217Z_05-sargabilidad.script.log`, regla 4; `.../20261027T172114Z_03-tipos-indice.script.log`, Q13 sin índice (1.486 buffers).

### 8.1.3. Coste de escritura y mantenimiento (G, H)

**10. INSERT con 4, 9 y 5 índices. ¿Cuáles rechazamos y con qué datos?**

Para 2.000 `INSERT` se midieron **10,1 bloques modificados por fila** con los **4 índices iniciales**, **20,2** con los **9 índices** propuestos por el compañero y **12,2** con los **5 índices finales V005**. Se rechazaron como innecesarios `IX_PED_CANAL` (tres valores, selectividad media **33,33 %**), `IX_PED_FEC_CLI` (no usado durante las consultas habituales y solapado con fecha), `IX_PED_CLIENTE` como índice simple (redundante con el nuevo índice que empieza por `ID_CLIENTE`) y `IX_PED_IMPORTE` (no utilizado durante la ventana de observación); tampoco se dejó el índice general `IX_PED_ESTADO` del compañero: se prefirió el índice de pendientes, más pequeño para la consulta de interés. **Matiz:** el protocolo no elimina el índice `IX_PED_FECHA`, aunque se detectó que sería prefijo del candidato `IX_PED_FEC_CLI`, porque este candidato no se mantuvo. La medición de uso corresponde a la carga ensayada, no a todas las consultas futuras. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T172640Z_06-indices.script.log`, escenarios, preguntas 1–4 y V005.

**11. Distingue divisiones 50/50, 90/10 y patrón cola con los gráficos.**

En **`IX_AZAR`**, 200.000 claves aleatorias provocaron **595 divisiones**, ninguna 90/10; las hojas tenían ocupación irregular (**75,4 %** media), propia de divisiones aproximadamente 50/50. En **`IX_CRECIENTE`**, hubo **398 divisiones, todas 90/10**, y ocupación **99,9 %**: la inserción siempre llega al extremo derecho. En **`IX_COLA`**, tras insertar 200.000 mensajes, borrar 150.000 antiguos e insertar 50.000, quedaban **100.000 vivos**, pero el mapa de hojas mostraba el **extremo izquierdo vacío y el derecho lleno**: **261 hojas vacías** y **81.159 entradas borradas**. La búsqueda del siguiente mensaje pasó a **263 buffers** frente a **2** en el índice sano. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T173231Z_07a-crecimiento.script.log`; `.../20261027T173231Z_07b-patron-cola.script.log`; gráficos `07a-grafico-*` y `07b-grafico-IX_COLA-antes`.

**12. ¿Qué remedio elegirías en producción, durante el servicio, y por qué?**

Elegiría primero **`ALTER INDEX ... COALESCE`**, tras medir el problema: pasó de **462 a 201 hojas** y de **263 a 2 buffers** para «siguiente mensaje», sin reconstruir todo el índice ni requerir un segundo segmento grande. Su desventaja es que **no devuelve espacio al tablespace** (el segmento siguió en **4 MB**). Si también necesitara liberar espacio, estudiaría **`SHRINK SPACE`**, que bajó a **1,69 MB**, considerando restricciones del objeto. `REBUILD ONLINE` costaría más recursos y redo, por lo que no sería la primera opción. A largo plazo rediseñaría la cola con **particionamiento y retirada de particiones antiguas**. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T173231Z_07c-remedios.script.log`.

### 8.1.4. SCN, control files, redo y FRA (I–L)

**13. ¿Qué compara Oracle al abrir para decidir si hace falta recuperación?**

Compara el **SCN de checkpoint registrado en el control file** para cada datafile con el **SCN de checkpoint de su cabecera** y comprueba la consistencia requerida. Antes del checkpoint, el archivo 1 tenía **5.496.253** en ambas fuentes; tras forzar el checkpoint quedó en **5.504.236** en ambas. Los archivos de `PDB$SEED` seguían en **2.098.101**, coherente con su modo solo lectura. Si la cabecera va retrasada respecto a lo esperado, Oracle puede requerir recuperación con redo antes de abrir. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T173736Z_08-scn-checkpoint.script.log`, apartados 2 y 3.

**14. ¿Qué protege la multiplexación del control file en un mismo volumen y qué no? ¿Cómo se haría en producción?**

Tener **tres copias** protege frente a la pérdida o corrupción de **una sola copia**: en O.B borramos `control03.ctl`, el arranque falló con `ORA-00205` y lo reconstruimos copiando el `control01.ctl` sano. No protege si se pierde **todo el volumen Docker o el disco** que contiene las tres copias, porque comparten el mismo dominio de fallo. En producción ubicaría los miembros en **almacenamientos físicos independientes**, con backups RMAN, monitorización y recuperación ensayada. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T180130Z_14b-perdida-controlfile.script.log`; `.../20261027T173803Z_09-multiplexar-controlfile.script.log`.

**15. Explica CURRENT, ACTIVE e INACTIVE y los borrados rechazados.**

`CURRENT` es el grupo donde escribe ahora LGWR; `ACTIVE` contiene redo que todavía puede hacer falta para recuperación de instancia; `INACTIVE` ya no se necesita para esa recuperación (aunque en ARCHIVELOG debe atenderse también su archivado). En la prueba K, tras los cambios de log, **grupo 3 = CURRENT**, grupos **1 y 2 = ACTIVE**. Oracle rechazó borrar CURRENT (**`ORA-01623`**), retirar un miembro de CURRENT (**`ORA-01609`**) y borrar otro grupo que necesitaba archivarse (**`ORA-00350`**). Estas protecciones evitan destruir redo necesario o dejar una configuración insegura. Después activamos el miembro `redo01b.log` restante con otro switch; los **seis miembros** terminaron en estado OK. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T174416Z_10-redo.script.log`, apartados 2–4; comprobación posterior de `v$logfile`.

**16. Cadena de causas cuando la FRA se llena: desde ORA-19815 hasta el bloqueo de DML.**

Al acercarse la FRA a su límite, Oracle avisa mediante **`ORA-19815`**; si los archivados ya no caben, aparecen mensajes como **`ORA-19809`/`ORA-00257`** o errores de archivado relacionados. **ARCn** no consigue archivar el grupo de redo terminado, por lo que Oracle no puede reutilizarlo de forma segura. Cuando se necesitan grupos libres, las sesiones que generan cambios se quedan esperando **`log file switch (archiving needed)`** y parece que el DML «se cuelga». En nuestro ensayo se redujo temporalmente el límite y después se **restauró a 4.096 MB**, quedando la FRA en **1,8 MB usados** en ese momento; se comprobó el archivado de los grupos. No consta en el extracto un bloqueo prolongado de sesiones ni un `ORA-19815` capturado literalmente: la secuencia es el mecanismo estudiado, no un síntoma adicional inventado. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T174815Z_11-fra-llena.script.log`; `scripts/lab5/11-fra-llena.sql`; informe `15-healthcheck` (FRA 89/4.096 MB).

### 8.1.5. Undo, WAL y simulacros (M–P)

**17. «Los lectores no bloquean a los escritores», con evidencia 12.**

La sesión A cambió el estudiante **101** de `ACTIVO` a `EGRESADO` sin `COMMIT` y mantuvo un bloqueo **TM modo 3** sobre la tabla y **TX modo 6** sobre la fila. La sesión B pudo hacer un `SELECT` normal y siguió viendo **`ACTIVO`**, reconstruido desde undo: la lectura consistente no esperó a A. Pero cuando B pidió **`SELECT ... FOR UPDATE WAIT 3`**, sí intentó bloquear para escribir y obtuvo **`ORA-00054`**. Después del `COMMIT` de A, B vio `EGRESADO`; Flashback Query leyó de nuevo el antiguo `ACTIVO`, que el script restauró finalmente. La frase describe **lecturas consistentes ordinarias**, no que dos escritores de la misma fila nunca se bloqueen. **Evidencia:** `scripts/lab5/12-sesion-a.sql`, `scripts/lab5/12-sesion-b.sql`; salida de `12-lectura-consistente.sh` en la ejecución del apartado M.

**18. ¿Por qué DELETE genera más undo y por qué ROLLBACK genera redo?**

En 10.000 operaciones, `INSERT` consumió **139 bloques de undo**; `UPDATE`, **72**; `DELETE`, **427**. Para deshacer una inserción basta conservar información que permita retirar la fila nueva, mientras que para deshacer un borrado hay que conservar la fila anterior y los cambios necesarios de índices. `ROLLBACK` tampoco es una operación gratuita: **modifica bloques de datos y undo**, y esos cambios se protegen con redo para poder reconstruirlos tras una caída. Medimos redo del rollback de **358 KB** (INSERT), **751 KB** (UPDATE) y **4.701 KB** (DELETE). **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T174950Z_12-undo-y-redo.script.log`.

**19. ¿Dónde queda la durabilidad tras COMMIT y después de checkpoint?**

Justo después del **COMMIT**, la garantía reside en el **redo escrito en los online redo logs por LGWR**; los bloques de la tabla aún pueden estar sucios en el buffer cache. Nuestra prueba produjo **1.779 KB de redo**, **2 escrituras LGWR** y **0 bloques DBWn** en el paso `UPDATE + COMMIT`, con **231 bloques sucios**. Tras `ALTER SYSTEM CHECKPOINT`, DBWn escribió **346 bloques** y el recuento de bloques sucios de la tabla bajó a **0**. Así, el checkpoint acerca físicamente los datafiles al estado confirmado y acorta la recuperación, pero la durabilidad del commit no espera a ese checkpoint. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T174954Z_13-lgwr-dbwn.script.log`.

**20. Simulacro A: roll forward y roll back con 102, 103 y el alert log.**

Antes de `SHUTDOWN ABORT`, el estudiante **102** quedó en `EGRESADO` con `COMMIT` y el **103** pasó temporalmente a `INACTIVO` sin confirmar. Al arrancar, Oracle aplicó redo (**roll forward**) para reconstruir el estado necesario, conservando el cambio confirmado de 102, y deshizo la transacción pendiente (**roll back**) para que 103 continuase en **`ACTIVO`**. El alert log documenta `Beginning crash recovery`, lectura de **65 KB de redo**, **53 bloques** que requerían recuperación y `Completed crash recovery`. Después se devolvió 102 a `ACTIVO`; ambos quedaron limpios. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T175836Z_14a-caida-instancia.script.log`.

**21. Simulacros C y D: RTO/RPO y diferencias.**

En **C** se restauró una **copia en frío del volumen completo** después de `DROP TABLE ... PURGE`: **RTO medido 66 s** y **ventana potencial de pérdida de 1 s** entre la copia y el borrado; el log no demuestra una pérdida efectiva de una modificación confirmada, así que no corresponde afirmar «se perdió 1 s de datos». La tabla de **60.000 matrículas** reapareció. En **D** se borró el datafile **16** (`academia01.dbf`) y se hizo `RESTORE DATAFILE` + `RECOVER DATAFILE` con RMAN: **RTO 8 s y RPO observado 0**, pues sobrevivió el cambio confirmado del estudiante 104 **después del backup**, gracias al redo. Son distintos porque C repone un volumen completo hasta un punto anterior, mientras D restaura **solo el archivo afectado** y aplica los cambios posteriores. En D Oracle dejó temporalmente toda `FREEPDB1` en `MOUNTED` por `ORA-63999`. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T180945Z_14c-simulacro-restauracion.script.log`; `.../20261027T181656Z_14d-perdida-datafile.script.log`.

**22. Clasifica los errores ORA- del bloque 5 del runbook.**

- **`ORA-01113` (file 25 needs media recovery), `ORA-01110` (archivos 16–20 y 25) y `ORA-63999` (media failure):** **efectos de los simulacros**, sobre todo de la pérdida/restauración de datafile, registrados históricamente en el alert log. Exigen atención si aparecen de nuevo fuera del ensayo, pero tras las pruebas `FREEPDB1` terminó en `READ WRITE` y el verificador confirmó `TODO OK`.
- **`ORA-00800 [Set Priority Failed], LGWR`:** **ruido conocido del entorno contenedorizado** por restricciones de prioridad del proceso. Debe vigilarse en contexto, pero aquí no impidió servicio ni recuperación.

Por tanto, **no hay una incidencia activa acreditada por esas diez líneas**: son nueve registros del fallo de medio provocado y uno de prioridad del contenedor. **Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T182403Z_15-healthcheck.script.log`, bloque 5; `.../20261027T182407Z_16-verificacion-final.script.log` (`TODO OK`).

## 9. Simulacro de examen 1Z0-182 — S1 a S26

Cada respuesta indica letra, justificación breve y la parte del laboratorio relacionada. En las preguntas que piden dos opciones se consignan ambas.

| Pregunta | Respuesta | Justificación y parte donde se comprobó |
|---|---|---|
| **S1** | **B** | CF cercano a filas implica muchos accesos a bloques distintos al recorrer el índice; **E**, `IX_PED_CLIENTE` CF 999.041. |
| **S2** | **A y C** | Índice funcional sobre `UPPER(email)` o reescritura `email = LOWER(:e)` cuando se guarda normalizado; **D/F**, 1.486 → 4 buffers. |
| **S3** | **B** | Oracle convierte la columna `VARCHAR2` mediante `TO_NUMBER`, inutilizando el índice ordinario; **F**, Q3. |
| **S4** | **B** | Bitmap adecuado para baja cardinalidad, lectura analítica y pocas escrituras concurrentes; **D**, Q14. |
| **S5** | **B** | El optimizador puede recorrer por valores del prefijo izquierdo mediante `INDEX SKIP SCAN`; **D**, Q6. |
| **S6** | **B** | `INVISIBLE` permite observar planes sin el índice y revertir con `VISIBLE`; **G**, pregunta 5. |
| **S7** | **A y C** | `COALESCE` y `SHRINK SPACE` remedian hojas vacías sin `REBUILD` bloqueante; **H**, 263 → 2 buffers. |
| **S8** | **B** | `REVERSE` distribuye las inserciones secuenciales, a costa de búsquedas por rango; **H**, 4 → 878 buffers en la prueba de rango. |
| **S9** | **C** | Cambiar una columna no indexada no exige actualizar las claves de todos los índices; **G**, comparación de `UPDATE`. |
| **S10** | **B** | La altura depende del fan-out, influido por el tamaño de las entradas de rama; **C**, fan-out real ≈370. |
| **S11** | **A y C** | En una IOT la fila reside en el índice primario y se evita leer una tabla heap adicional; **D**, Q15. |
| **S12** | **B** | Se coteja checkpoint SCN del control file y la cabecera del datafile; **I**, evidencia 08. |
| **S13** | **C** | CKPT actualiza información de checkpoint en control files y cabeceras; DBWn escribe bloques; **I/N**. |
| **S14** | **B y E** | En NOMOUNT están disponibles estado de instancia y parámetros de arranque; no aún control file/diccionario; **Lab 4**, arranque por etapas. |
| **S15** | **B** | Se cambia a ARCHIVELOG con base montada, luego se abre; **L**, ya estaba activado y el script evitó repetir el cambio. |
| **S16** | **B** | Un grupo INACTIVE ya archivado y perdido puede recrearse con `ALTER DATABASE CLEAR LOGFILE GROUP n`, tras verificar que no requiere recuperación; **K**, reglas de gestión redo (caso teórico, no se destruyó ese grupo). |
| **S17** | **A y C** | Undo sirve para lectura consistente y Flashback Query además de rollback; **M**, estudiante 101. |
| **S18** | **B** | Los cambios de bloques undo también necesitan redo para reconstruirlos antes de revertir transacciones no confirmadas; **M**, 12-undo-y-redo. |
| **S19** | **A** | Tras `Commit complete`, LGWR ha hecho durable el redo online, no necesariamente el datafile; **N**, cero bloques DBWn tras COMMIT. |
| **S20** | **A** | Un objetivo MTTR menor fuerza trabajo de checkpoint incremental para facilitar recuperación más breve; **I/N** (principio estudiado, parámetro no modificado). |
| **S21** | **B** | ARCn no puede archivar los grupos, por ejemplo porque la FRA está llena; **L**, simulación de reducción de FRA. |
| **S22** | **B** | Ante pérdida de datafile no esencial, ponerlo offline puede aislar el daño antes de restaurarlo; **O.D**, script contempla PDB cerrada. |
| **S23** | **B** | SYSTEM exige restauración con base montada y recuperación antes de abrir; **O.D**, extrapolación de recuperación de archivo, no se destruyó SYSTEM. |
| **S24** | **B** | En NOARCHIVELOG no hay cadena de archivados para rehacer todo lo posterior al backup; **L/O**, contraste con recuperación RMAN en ARCHIVELOG. |
| **S25** | **B y D** | Más capacidad/retención undo y, si procede, `RETENTION GUARANTEE` para consultas críticas; **M**, `undo_retention=900`, ORA-01555=0. |
| **S26** | **A** | `V$RECOVERY_AREA_USAGE` desglosa la FRA por tipo de archivo; **L**, consulta de `ARCHIVED LOG`. |

## Tabla de los cuatro simulacros — RTO / RPO

| Simulacro | Fallo y recuperación | RTO observado | RPO y datos recuperados | Evidencia |
|---|---|---|---|---|
| **O.A** | `SHUTDOWN ABORT` → crash recovery automática | **No cronometrado** como intervalo completo; el script informa `t=0s` al comprobar `healthy`, que no es un RTO íntegro | **0 para la transacción confirmada**: 102 se conserva; transacción 103 sin confirmar revertida | `20261027T175836Z_14a-caida-instancia.script.log` |
| **O.B** | Borrado de `control03.ctl` → copiar `control01.ctl` y abrir | **No cronometrado** como intervalo completo; `healthy` informó `t=0s` tras reparar | **0 datos perdidos**, control files 3/3 | `20261027T180130Z_14b-perdida-controlfile.script.log` |
| **O.C** | `DROP ... PURGE` → restauración de copia en frío completa | **66 s** | **Ventana potencial 1 s** desde backup al fallo, sin pérdida efectiva medida | `20261027T180945Z_14c-simulacro-restauracion.script.log` |
| **O.D** | Desaparición de `academia01.dbf` → RMAN RESTORE + RECOVER | **8 s** | **0**, sobrevivió la modificación posterior al backup del estudiante 104 | `20261027T181656Z_14d-perdida-datafile.script.log` |

Las evidencias de esta tabla están bajo `docs/bitacora/lab5/evidencia/script/`. La verificación global `20261027T182407Z_16-verificacion-final.script.log` terminó en **`RESULTADO: TODO OK`**.

## Retrospectiva sin culpables — FRA llena (Parte L.3)

**Incidente simulado.** Se redujo de forma deliberada el espacio de la FRA para reproducir una situación de presión de archivado. El mecanismo de riesgo es que ARCn no pueda conservar redo antiguo y los cambios queden esperando un grupo reutilizable (`log file switch (archiving needed)`).

**Impacto observado.** La salida que conservamos muestra grupos y estado de archivado durante la reducción, y la recuperación del límite a **4.096 MB**; **no acredita** una pérdida de transacciones ni un bloqueo prolongado de una sesión de aplicación. Tras la reparación, el script midió **1,8 MB** usados; el healthcheck posterior registró **89/4.096 MB (2,2 %)** y base disponible.

**Detección y diagnóstico.** Revisaríamos `V$RECOVERY_FILE_DEST`, `V$RECOVERY_AREA_USAGE`, `V$LOG`, `V$SESSION` y alert log, atendiendo especialmente a mensajes como `ORA-19815`, `ORA-00257` y al evento `log file switch (archiving needed)`.

**Causa raíz del simulacro.** Límite de la FRA reducido artificialmente a un nivel incompatible con la generación de redo, no un crecimiento normal del negocio en esta ejecución.

**Mitigación ejecutada.** `ALTER SYSTEM SET db_recovery_file_dest_size = 4G SCOPE=BOTH`; se comprobó el valor final y que el archivado volvía a funcionar. En producción, antes de borrar archivados, verificaríamos la política de retención y copias RMAN: borrar sin respaldo puede impedir recuperación de medios.

**Cambios preventivos.** Alertas de ocupación (por ejemplo, **80 %**), vigilar la tasa de archivado y crecimiento, asegurar capacidad y retención suficientes, ensayar restauraciones y documentar un procedimiento de actuación. **Lección:** reaccionar a los avisos de capacidad antes de que ARCn deje de completar archivados.

**Evidencia:** `docs/bitacora/lab5/evidencia/script/20261027T174815Z_11-fra-llena.script.log`, `20261027T182403Z_15-healthcheck.script.log`.

## Retrospectiva de los simulacros de recuperación (Parte O)

**Qué funcionó.** La recuperación de instancia conservó el cambio confirmado y revirtió el pendiente; la multiplexación permitió sustituir el control file perdido; Flashback resolvió el borrado sin `PURGE`; el backup completo restauró las 60.000 matrículas; RMAN recuperó el datafile y conservó el cambio confirmado después del backup. La comprobación final confirmó TiendaSur, los índices V005, control files, FRA y ausencia de objetos de prueba.

**Qué sorprendió.** Durante O.D Oracle **cerró toda FREEPDB1 y la dejó `MOUNTED`** (`ORA-63999`) al detectar el archivo perdido. El plan de recuperación tuvo que esperar a un estado estable, ejecutar RMAN y reabrir la PDB. La disponibilidad afectada fue mayor que la del único tablespace.

**Qué mejoraríamos.** Instrumentar la medición de RTO de O.A y O.B desde el instante de fallo hasta el retorno efectivo del servicio, sin confundir `t=0s` de `esperar-healthy.sh` con el RTO global; preferir respaldos RMAN y recuperación de medios para limitar RPO, situar copias de control files en discos independientes, vigilar FRA y mantener simulacros periódicos con alertas comprobables.

**Conclusión.** El objetivo técnico se alcanzó: el Lab 5 finalizó con **`TODO OK`**, **RTO de 66 s** en restauración completa y **8 s** en recuperación de datafile, con **RPO observado 0** en O.D. Estas cifras son propias del banco de laboratorio, no garantías universales de producción.
