# Runbook — Recuperación de un datafile perdido

## 1. Objetivo

Documentar el procedimiento de diagnóstico y recuperación de un datafile perdido en Oracle Database Free mediante RMAN, minimizando el tiempo de indisponibilidad y evitando la pérdida de transacciones confirmadas.

## 2. Entorno

- Contenedor Docker: `oralab-26ai`.
- Base CDB: `FREE`.
- PDB: `FREEPDB1`.
- Modo: `ARCHIVELOG`.
- FRA: `/opt/oracle/oradata/fra`.
- Tablespace de prueba: `TBS_ACADEMIA`.
- Datafile: `/opt/oracle/oradata/FREE/FREEPDB1/academia01.dbf`.

## 3. Detección del incidente

Los síntomas observados durante el simulacro fueron:

- `ORA-01116`: error al abrir el datafile.
- `ORA-01110`: identificación del archivo afectado.
- `ORA-27041`: error de acceso al archivo físico.
- `ORA-63999`: fallo de medio detectado por Oracle.

Durante el ejercicio, Oracle cerró la PDB `FREEPDB1`, dejándola en estado `MOUNTED`.

## 4. Diagnóstico inicial

Comprobar el estado de la base y los archivos:

```sql
SELECT name, open_mode FROM v$pdbs;

SELECT file#, name, status
FROM v$datafile
ORDER BY file#;
```

Identificar el archivo afectado y revisar el alert log antes de iniciar la recuperación.

## 5. Procedimiento de recuperación

Este procedimiento requiere una copia RMAN válida y los redo necesarios para recuperar el archivo.

### Paso 1. Comprobar la copia de seguridad

En RMAN:

```rman
LIST BACKUP OF DATAFILE 16;
```

El número 16 corresponde al datafile afectado durante nuestro simulacro. En otro incidente debe identificarse el número real.

### Paso 2. Recuperar el archivo mediante RMAN

```rman
RESTORE DATAFILE 16;
RECOVER DATAFILE 16;
```

`RESTORE` recupera el contenido respaldado. `RECOVER` aplica los cambios registrados posteriormente en redo.

### Paso 3. Devolver el archivo a servicio

Cuando corresponda, conectar a `FREEPDB1`:

```sql
ALTER SESSION SET CONTAINER = FREEPDB1;
ALTER DATABASE DATAFILE 16 ONLINE;
```

Si `FREEPDB1` permanece montada, desde `CDB$ROOT`:

```sql
ALTER PLUGGABLE DATABASE FREEPDB1 OPEN;
```

Estos pasos se deben realizar de acuerdo con el estado real de la PDB. No deben ejecutarse automáticamente sin comprobar que RMAN ha terminado correctamente.

## 6. Verificación posterior

Comprobar que:

1. La PDB vuelve a estar en `READ WRITE`.
2. El datafile está disponible.
3. Las consultas a las tablas afectadas funcionan.
4. Los cambios confirmados posteriores al backup se han recuperado.
5. No existen errores de recuperación pendientes.

## 7. Resultados reales del simulacro O.D

El 27 de octubre de 2026 se eliminó deliberadamente el archivo `academia01.dbf` después de realizar una copia RMAN y confirmar una modificación del estudiante 104.

Los resultados fueron:

| Métrica | Resultado |
|---|---|
| Datafile afectado | 16 |
| Estado de la PDB durante el fallo | MOUNTED |
| Recuperación | RMAN RESTORE + RECOVER |
| RTO medido | 8 segundos |
| RPO observado | 0 |
| Estudiantes recuperados | 20.000 |
| Matrículas conservadas | 60.000 |
| Estado final | READ WRITE |

La modificación confirmada después del backup sobrevivió a la recuperación, lo que demuestra la aplicación correcta del redo.

## 8. Prevención y recomendaciones

- Mantener copias RMAN verificadas.
- Conservar los redo archivados necesarios para la recuperación.
- Supervisar el espacio disponible en la FRA.
- Mantener multiplexados los control files y los grupos de redo.
- Documentar los incidentes y medir RTO y RPO.
- Realizar periódicamente simulacros de restauración.

## 9. Evidencias

Consultar:

- `scripts/lab5/14d-perdida-datafile.sh`.
- `docs/bitacora/lab5/evidencia/script/20261027T181656Z_14d-perdida-datafile.script.log`.
- `docs/bitacora/lab5-respuestas.md`.

**Conclusión:** el procedimiento RMAN permitió recuperar el datafile perdido, mantener los datos confirmados y restablecer el servicio en 8 segundos durante el simulacro.
