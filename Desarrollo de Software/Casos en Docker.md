

# Caso 1
Claro, te explico paso a paso y con mucho detalle cómo hacer para que tu amigo pueda tener la misma base de datos PostgreSQL con los mismos datos que tú tienes, usando Docker y GitHub. La idea es que tu amigo no tenga que instalar nada complicado, solo usar Docker para levantar la app y la base de datos con los datos ya cargados.

---

## 1. ¿Qué pasa con la base de datos cuando usas Docker?

Cuando usas Docker para tu app con PostgreSQL, la base de datos corre dentro de un contenedor, que es como una cajita. Pero si borras esa cajita, también se borran los datos que estaban dentro, a menos que uses un **volumen**.

- El **volumen** es un lugar especial en tu computadora donde Docker guarda los datos de la base de datos, fuera de la cajita.
    
- Así, si borras la cajita (contenedor), los datos siguen ahí en el volumen.
    
- Pero ese volumen está en tu computadora, no dentro del contenedor ni en GitHub.
    

---

## 2. ¿Cómo compartir la base de datos con tu amigo?

Tu amigo va a descargar tu app desde GitHub y va a usar Docker para levantar la app y la base de datos. Pero el volumen con los datos no se sube a GitHub, porque es un espacio local de tu computadora.

Entonces, para que tu amigo tenga la base de datos con los mismos datos que tú, tienes que **exportar** o **hacer un respaldo** de la base de datos y que él lo importe en su contenedor.

---

## 3. Paso a paso detallado para compartir la base de datos con Docker

## Paso 1: Crear un respaldo (backup) de tu base de datos

Desde tu computadora, donde tienes el contenedor PostgreSQL corriendo, haces un respaldo de todos los datos en un archivo `.sql`. Esto es como sacar una foto de toda la base de datos para poder copiarla.

Ejemplo de comando para hacer el backup:

bash

`docker exec -t postgres-db pg_dumpall -c -U tu_usuario > backup.sql`

- `postgres-db` es el nombre del contenedor donde corre PostgreSQL.
    
- `pg_dumpall` es la herramienta que crea el respaldo.
    
- `backup.sql` es el archivo que se crea con todos los datos y estructura de la base.
    

Este archivo `backup.sql` es un archivo de texto que contiene todas las instrucciones para recrear la base de datos con sus tablas y registros.

---

## Paso 2: Subir tu app a GitHub sin subir la base de datos

Tu repositorio GitHub debe contener:

- El código de tu app.
    
- El `Dockerfile` o `docker-compose.yml` para levantar la app y la base de datos.
    
- El archivo `backup.sql` que hiciste en el paso anterior (opcional, para que tu amigo pueda restaurar la base).
    

No subas el volumen ni los datos binarios, solo el respaldo en `.sql`.

---

## Paso 3: Dockerizar tu app y la base de datos con un archivo `docker-compose.yml`

Para que sea fácil levantar todo, crea un archivo `docker-compose.yml` que defina:

- El servicio de PostgreSQL con un volumen para persistir datos.
    
- El servicio de tu app que se conecte a la base de datos.
    

Ejemplo básico:

text

`version: '3.8' services:   db:    image: postgres:17.4    environment:      POSTGRES_USER: tu_usuario      POSTGRES_PASSWORD: tu_contraseña      POSTGRES_DB: tu_basedatos    volumes:      - pgdata:/var/lib/postgresql/data    ports:      - "5432:5432"   app:    build: .    depends_on:      - db    ports:      - "3000:3000"    environment:      DB_HOST: db      DB_USER: tu_usuario      DB_PASSWORD: tu_contraseña      DB_NAME: tu_basedatos volumes:   pgdata:`

- El volumen `pgdata` guarda los datos de PostgreSQL en la máquina local.
    
- Tu amigo solo tiene que ejecutar `docker-compose up` para levantar todo.
    

---

## Paso 4: Instrucciones para tu amigo para restaurar la base de datos

Cuando tu amigo descargue el repositorio, hará esto:

1. Levanta los contenedores con:
    

bash

`docker-compose up -d`

2. Para que la base de datos tenga los datos que tú tenías, debe importar el archivo `backup.sql` que le diste.
    

Ejemplo para importar el backup:

bash

`cat backup.sql | docker exec -i nombre_contenedor_db psql -U tu_usuario -d tu_basedatos`

- `nombre_contenedor_db` es el nombre o id del contenedor PostgreSQL que está corriendo (puede verlo con `docker ps`).
    
- Esto carga todos los datos y tablas que tú tenías en la base de datos de tu amigo.
    

---

## Paso 5: Verificar que la base de datos tiene los mismos datos

Tu amigo puede usar herramientas como `psql` dentro del contenedor o programas externos (pgAdmin, DBeaver) para conectarse a la base y ver que los datos están igual que en tu máquina.

---

## Resumen final

|Paso|Qué haces|Por qué|
|---|---|---|
|1|Haces un backup de la base de datos en un archivo `.sql`|Para guardar los datos en un archivo que puedas compartir|
|2|Subes tu app y el archivo `.sql` a GitHub (no el volumen)|Para que tu amigo tenga todo el código y el respaldo|
|3|Creas un `docker-compose.yml` que levante la app y PostgreSQL con volumen|Para que tu amigo pueda levantar todo fácilmente con Docker|
|4|Tu amigo levanta los contenedores y restaura la base con el archivo `.sql`|Para que la base tenga los mismos datos que tú tenías|
|5|Tu amigo usa la app con la base de datos ya cargada|Todo funciona igual que en tu máquina|

---

## ¿Por qué no se puede subir el volumen directamente?

Porque el volumen es un espacio especial en tu computadora, no un archivo común. Es como un baúl gigante que Docker usa para guardar datos. No se puede subir a GitHub porque no es un archivo, sino una carpeta oculta y con datos binarios que no deben ir al repositorio.

Por eso se usa el respaldo `.sql`, que es un archivo de texto que puede copiarse, subirse y compartirse fácilmente.

---

## Extra: ¿Cómo crear el backup y restaurar con comandos completos?

**Para crear backup:**

bash

`docker exec -t postgres-db pg_dumpall -c -U tu_usuario > backup.sql`

**Para restaurar backup en otra máquina:**

bash

`cat backup.sql | docker exec -i postgres-db psql -U tu_usuario -d tu_basedatos`

---

Con estos pasos, tú y tu amigo pueden compartir la app y la base de datos con todos los datos, sin complicaciones, usando Docker y GitHub. Así se asegura que la app funcione igual en ambas computadoras.

Si quieres, puedo ayudarte a crear los archivos exactos o explicarte cómo hacer cada comando con más detalle.

1. [https://www.datacamp.com/es/tutorial/postgresql-docker](https://www.datacamp.com/es/tutorial/postgresql-docker)
2. [https://imaginaformacion.com/tutoriales/los-volumenes-de-docker](https://imaginaformacion.com/tutoriales/los-volumenes-de-docker)
3. [https://www.youtube.com/watch?v=F6zlG-jtFHg](https://www.youtube.com/watch?v=F6zlG-jtFHg)
4. [https://kinsta.com/es/blog/volumenes-docker-compose/](https://kinsta.com/es/blog/volumenes-docker-compose/)
5. [https://labex.io/es/tutorials/docker-how-to-persist-data-in-docker-volumes-493636](https://labex.io/es/tutorials/docker-how-to-persist-data-in-docker-volumes-493636)
6. [https://geoinnova.org/blog-territorio/postgresql-y-pgadmin-con-docker/](https://geoinnova.org/blog-territorio/postgresql-y-pgadmin-con-docker/)
7. [https://www.reddit.com/r/docker/comments/a5lvk7/create_volume_for_persistent_postgres_local/?tl=es-419](https://www.reddit.com/r/docker/comments/a5lvk7/create_volume_for_persistent_postgres_local/?tl=es-419)
8. [https://bonisql.com/2021/02/28/bases-de-datos-en-contendores-postgresql/](https://bonisql.com/2021/02/28/bases-de-datos-en-contendores-postgresql/)