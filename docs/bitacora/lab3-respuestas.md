# Lab 3 - Respuestas de comprobación

## Docker

### 1. ¿Qué diferencia hay entre una imagen y un contenedor?

Una imagen es la plantilla a partir de la cual Docker crea los contenedores. Es de solo lectura y contiene todo lo necesario para ejecutar una aplicación.

Un contenedor es una instancia creada a partir de esa imagen. Por ejemplo, en G2 ejecuté la imagen `hello-world` y Docker creó un contenedor que terminó al acabar su tarea. En G4 utilicé la imagen `alpine:3.20` para crear un contenedor llamado `prueba` y pude entrar dentro de él con una shell.

### 2. ¿Por qué en G5 desapareció nota.txt y en G6 no?

En G5 guardé `nota.txt` dentro del propio sistema de archivos del contenedor. Cuando eliminé ese contenedor, también desaparecieron sus datos.

En G6 el archivo se guardó dentro del volumen `datos-prueba`. Los volúmenes son independientes de los contenedores, por lo que pude eliminar un contenedor, crear otro y seguir leyendo el mismo archivo.

### 3. Diferencia entre docker ps y docker ps -a. ¿Qué significa Exited (0)?

`docker ps` muestra solamente los contenedores que están ejecutándose en ese momento.

`docker ps -a` también muestra los que ya han terminado o están detenidos.

`Exited (0)` significa que el proceso principal del contenedor terminó correctamente, sin errores. El 0 es el código de salida que indica éxito.

### 4. En -p 8181:8181, ¿qué puerto es de mi equipo y cuál del contenedor?

El número de la izquierda corresponde al equipo anfitrión y el de la derecha al contenedor.

Por tanto:

`-p 8181:8181`

publica el puerto 8181 de mi equipo hacia el puerto 8181 del contenedor.

En `-p 80:8080`, accedería al puerto 80 de mi equipo y Docker enviaría el tráfico al puerto 8080 del contenedor. En el caso de nginx que usamos en la práctica no funcionaría así por defecto, porque nginx estaba escuchando en el puerto 80 del contenedor, no en el 8080.

### 5. ¿Por qué Oracle se queda en marcha y hello-world termina?

Un contenedor permanece funcionando mientras su proceso principal siga activo.

`hello-world` simplemente imprime un mensaje y termina, por lo que su contenedor también termina.

Oracle, en cambio, mantiene en ejecución los procesos del servidor de base de datos, así que el contenedor permanece activo mientras Oracle esté funcionando.

### 6. ¿Qué es el digest y por qué lo registramos si usamos :latest?

El digest es una identificación exacta de una imagen, normalmente mediante un valor SHA-256.

`:latest` es solamente una etiqueta y puede apuntar a una imagen diferente en el futuro. Guardando el digest sabemos exactamente qué versión binaria utilizamos, aunque la etiqueta `latest` cambie más adelante.

### 7. ¿Qué comando borraría realmente los datos de Oracle?

Los datos persistentes están en el volumen `oralab-26ai-data`. Por tanto, eliminar solamente el contenedor con:

`docker rm oralab-26ai`

no elimina los datos.

Lo que realmente los borraría sería eliminar el volumen, por ejemplo:

`docker volume rm oralab-26ai-data`

Por eso hay que tener especial cuidado con comandos como `docker system prune --volumes`.

## Git, organización y evidencia

### 8. ¿Por qué hacemos el laboratorio dentro del repositorio y con Issue, branch y Pull Request?

Porque no solo interesa que Oracle funcione, sino que quede registrado cómo se ha creado el entorno.

El Issue explica qué trabajo se quiere realizar, la branch mantiene los cambios separados de `main`, los commits documentan cada etapa y el Pull Request permite revisar todo antes de incorporarlo.

De esta forma el entorno es reproducible, revisable y queda un historial de lo que se hizo.

### 9. Diferencia entre source 00-config.sh y bash 00-config.sh

`bash 00-config.sh` ejecutaría el script en un proceso de Bash separado. Cuando ese proceso terminase, las variables que haya definido desaparecerían para mi terminal actual.

`source 00-config.sh` ejecuta el contenido dentro de la shell actual, por lo que variables como `CONT_NAME`, `EVID` o `SERVICE_PDB` quedan disponibles para los comandos siguientes.

Por eso en esta práctica utilizamos `source`.

### 10. Explica 20260915T091230Z_02-docker.script.log

`20260915T091230Z` es la fecha y hora UTC en formato ISO 8601: 15 de septiembre de 2026 a las 09:12:30. La `Z` indica UTC.

`02` identifica el número de evidencia.

`docker` describe qué se estaba verificando.

`script.log` indica que es una evidencia procedente de la terminal o de un script.

Esta nomenclatura permite ordenar las evidencias y saber qué se hizo y cuándo.

### 11. ¿Para qué sirve .gitattributes?

`.gitattributes` permite definir cómo debe tratar Git determinados tipos de archivo.

En esta práctica fuerza finales de línea LF para scripts y SQL. Esto evita problemas al trabajar entre Windows y Linux, especialmente errores provocados por CRLF como `$'\r': command not found`, además de evitar cambios innecesarios en los diffs.

### 12. ¿Por qué usamos Create a merge commit y no Squash and merge?

Durante esta práctica cada commit representa una parte concreta del trabajo y tiene valor por sí mismo: instalación, verificación, migraciones, ORDS, evidencias, etc.

Si hiciéramos squash, todo ese historial se convertiría en un único commit.

Con `Create a merge commit` se conserva la secuencia completa y se puede saber cuándo se realizó y verificó cada parte del laboratorio.

## Seguridad

### 13. Explica las cuatro capas de la estrategia de contraseñas

La primera capa es añadir `config/.env` a `.gitignore`, para impedir que Git pueda versionar el archivo con las contraseñas reales.

La segunda es tener `config/.env.example`, que sí se versiona pero solamente contiene valores de ejemplo.

La tercera es tener un `config/.env` local con los secretos reales.

La cuarta consiste en cargar esas variables en tiempo de ejecución para que los scripts utilicen las contraseñas sin escribirlas directamente en el código.

Si me saltase la primera capa podría añadir por error `config/.env` a Git y dejar las contraseñas guardadas en el historial.

### 14. ¿Por qué no ponemos la contraseña directamente en docker run?

Aunque un script no se vaya a subir a Git, escribir una contraseña directamente en un comando sigue siendo una mala práctica.

Puede quedar almacenada en el historial de la terminal, aparecer mientras se inspeccionan procesos o terminar copiada en una captura o evidencia.

Es más seguro cargarla desde un archivo local protegido como `config/.env` y utilizar la variable correspondiente.

### 15. ¿Basta con borrar una contraseña en un commit nuevo si ya se publicó?

No. Aunque se elimine en un commit nuevo, la contraseña seguirá existiendo en los commits anteriores del historial.

Una credencial publicada debe considerarse comprometida. Hay que cambiarla o rotarla y, además, limpiar el historial si es necesario. Si ya se ha publicado en el repositorio remoto, también habría que avisar al responsable o docente.

## Oracle y herramientas

### 16. ¿Por qué no usamos SPOOL ni @archivo.sql con SQL*Plus dentro del contenedor?

El `sqlplus` de la Parte J se estaba ejecutando dentro del contenedor.

Si utilizase `SPOOL`, el fichero se escribiría dentro del sistema de archivos del contenedor y no directamente en mi repositorio.

De la misma forma, `@archivo.sql` buscaría el fichero dentro del contenedor, aunque realmente estuviera en Ubuntu.

Por eso enviamos el SQL mediante redirección de entrada `<` y utilizamos `tee` desde el equipo anfitrión para guardar la salida en el repositorio.

### 17. ¿Qué hace WHENEVER SQLERROR EXIT SQL.SQLCODE?

Hace que SQL*Plus termine inmediatamente cuando aparece un error SQL y devuelva como código de salida el código del error de Oracle.

De esa forma, si una migración falla, el script de Bash puede detectar el error y detener el proceso.

Sin esa instrucción podrían seguir ejecutándose sentencias posteriores y acabaríamos con una migración aplicada solamente a medias.

### 18. ¿Qué es una migración y por qué V000 y V001 no deben editarse una vez aplicadas?

Una migración es un cambio versionado de la estructura o configuración de la base de datos.

En esta práctica V000 crea los tablespaces y usuarios y V001 crea los esquemas y tablas.

Una migración ya aplicada no debería modificarse porque distintos equipos podrían tener versiones diferentes de una migración con el mismo nombre. Para realizar otro cambio se debe crear una nueva migración con un número posterior.

### 19. ¿Por qué usamos FREEPDB1 en SQL Developer?

`FREEPDB1` es la PDB de trabajo donde hemos creado nuestros usuarios y esquemas.

Usar `FREE` nos llevaría al contenedor raíz de Oracle en lugar de a la PDB donde se desarrolla el laboratorio.

Además estamos utilizando un `Service name`, no un SID, porque la conexión debe dirigirse específicamente al servicio de `FREEPDB1`.

### 20. ¿Qué aporta SQLcl frente a SQL*Plus y por qué hay que conocer ambos?

SQL*Plus es una herramienta clásica, sencilla y disponible prácticamente en cualquier instalación de Oracle. Es muy útil cuando solamente se dispone de una terminal en un servidor.

SQLcl es una herramienta moderna que añade características como mejor formato de salida, historial, autocompletado, gestión de conexiones e integración con herramientas de migración.

Un DBA debe conocer SQL*Plus porque puede encontrárselo en cualquier servidor y SQLcl porque es más cómodo y potente para el trabajo diario.

## Entorno de trabajo

### 21. ¿Por qué pasamos de Git Bash a Ubuntu en WSL 2?

Ubuntu en WSL 2 proporciona un entorno Linux real y mucho más parecido al de los servidores que se utilizan profesionalmente.

Con Git Bash pueden aparecer incompatibilidades con herramientas y scripts pensados para Linux. También hay programas de administración que no están disponibles de la misma forma y existen diferencias de rutas, permisos y comportamiento del sistema.

Con WSL 2 podemos utilizar herramientas estándar como `apt`, `ss`, `tmux`, `shellcheck` o las versiones Linux de SQLcl y ORDS.

### 22. ¿Por qué clonamos en ~/oracle-database-lab y no en /mnt/c? ¿Y por qué usamos bash?

El repositorio se guarda dentro del sistema de archivos Linux porque trabajar directamente sobre `/mnt/c` implica acceder constantemente al sistema de archivos de Windows desde WSL. Eso puede ser más lento y puede generar diferencias de permisos, metadatos y comportamiento de archivos.

`~/oracle-database-lab` se encuentra en el sistema de archivos nativo de Linux y ofrece un comportamiento más parecido al de un servidor real.

Usamos Bash porque es la shell utilizada en los scripts de la práctica y es una opción estándar en servidores Linux. Utilizar la misma shell reduce diferencias de sintaxis y configuración entre alumnos y evita problemas producidos por configuraciones particulares de otras shells como zsh.
