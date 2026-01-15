# Conexión de PostgreSQL con Python


Sino está instalado pip python3
```bash
sudo apt-get install python3-pip
```

```bash
apt-get update
```

```bash
sudo apt-get install libpq-dev python3-dev
```

```bash
sudo apt install python3-psycopg2
```


```sql
create user owner2 with createdb password '12345';
```

Ingresar con usuario owner 2

```sql
create database bdconexion;
```

Usar la base de datos `bdconexion`. Luego crear la tabla docente
```sql
create table docente(
id int,
nombre varchar(80),
sueldo float);
```

Crear archivo config.py
```python
#config.py
user="owner2"
password="12345"
database="bdconexion"
host="localhost"
port=5432
```

Crear archivo prueba_conexion.py
```python
#prueba_conexion.py
import psycopg2
import config
import traceback

def connect():
    try:
        connection=psycopg2.connect(
            user=config.user,
            password=config.password,
            database=config.database,
            host=config.host,
            port=config.port,
            )
        return connection
    except Exception as err:
        print("Error ocurrido al crear una conexion...")
        traceback.print_exc()

def print_version(connection):
    cursor = connect().cursor()
    cursor.execute('SELECT version()')
    db_version=cursor.fetchone()
    print(db_version)
    cursor.close()
    connection.close()
    
    
###Prog Principal
if __name__ == '__main__':
    print_version(connect())
```

Luego ejecutar el archivo
```bash
python3 prueba_conexion.py
```


Crear archivo ejercicio3.py. Este archivo crea la tabla estudiante
```python
#ejercicio3.py
import psycopg2
import config
import traceback
def connect():
  try: 
      connection= psycopg2.connect(
                     user= config.user,
                     password=config.password,
                     database=config.database,
                     host=config.host,
                     port=config.port
                  )
      return connection
  except Exception as err:
      print("Error ocurrido al crear una conexion...")
      traceback.print_exc()
def creaTabla(connection):
     cursor=connection.cursor()
     query="""
          CREATE TABLE estudiante(
                         idest int primary key,
                         nombres varchar(100),
                         apellidos varchar(100),
                         ciudad varchar(100));
          """
     try:
       cursor.execute(query)
       connection.commit()
       print("La tabla se creo con exito")
     except Exception as err:
       print(err)
     cursor.close()
     connection.close()

####Prog Principal
if __name__=='__main__':
    creaTabla( connect() )
```
Luego ejecutar
```bash
python3 ejercicio3.py
```

Crear archivo ejercicio4.py. Este archivo inserta una tupla en la tabla estudiante.
```python
#Ejercicio4.py
import psycopg2
import config
import traceback

def connect():
  try: 
      connection= psycopg2.connect(
                     user= config.user,
                     password=config.password,
                     database=config.database,
                     host=config.host,
                     port=config.port
                  )
      return connection
  except Exception as err:
      print("Error ocurrido al crear una conexion...")
      traceback.print_exc()

def insertaTupla(connection):
    cursor = connection.cursor()
    query = """
            insert into estudiante(idest, nombres, apellidos, ciudad)
            values (%s, %s, %s, %s);
            """
    try:
        data = (1, "Ashley", "Bravo", "Huancayo")
        cursor.execute(query, data)
        connection.commit()
        print("Tupla se inserto con exito")
    except Exception as err:
        print(err)
    cursor.close()
    connection.close()
        
### Prog Principal
if __name__ == '__main__':
    insertaTupla(connect())
```

Luego ejecutar

```bash
python3 ejercicio4.py
```



# Crear backup


## Tipo sql

En línea de comandos o power shell

```bash
pg_dump -U <usuario> -d <nombre-BD> -f "ruta\nombre" o nombre
```

Ejemplo
```bash
pg_dump -U postgres -d sigepat -f "C:\Users\mitch\Documents\sigepat_backup.sql"

```


## Tipo backup

Ejecuta el siguiente comando desde la terminal o desde una sesión de `psql`:
```bash
pg_dump -U postgres -F c -d sigepat -f /ruta/donde/guardar/sigepat.backup
```

- `-U postgres`: Usuario propietario de la base de datos (puedes cambiarlo si es necesario).
- `-F c`: Indica el formato de salida **custom** (binario compatible con pgAdmin).
- `-d sigepat`: Nombre de la base de datos que deseas respaldar.
- `-f /ruta/donde/guardar/sigepat.backup`: Ruta completa y nombre del archivo de respaldo

Ejemplo
```shell
pg_dump -U postgres -F c -d sigepat -f sigepat_backup.backup
```


## Restaurar achivo sql en bd creada en neon:

Ejecutar el comando psql en un terminal:
```shell
psql "postgresql://sigepat-bd_owner:Ulxwnb3rj8Rz@ep-orange-bird-a5o6nkrk.us-east-2.aws.neon.tech/sigepat-bd?sslmode=require" -f "C:\Users\mitch\Documents\sigepat_backup.sql"
```


# Cambiar tipo de dato

```sql
ALTER TABLE <nombre_tabla>
ALTER COLUMN <nombre_columna> TYPE <nuevo_tipo>
USING <nombre_columna>::<nuevo_tipo>;
```

Ejemplo

- Tabla: capitulo
- Columna: descripcion (tipo INT)

Convertir a VARCHAR(255)

```sql
ALTER TABLE capitulo
ALTER COLUMN descripcion TYPE VARCHAR(255)
USING descripcion::VARCHAR(255);
```

> [!tip]
> `USING descripcion::VARCHAR(255)` le dice a PostgreSQL cómo convertir los valores actuales. Es obligatorio cuando el tipo anterior y el nuevo no son compatibles.
> Si tuvieras datos, PostgreSQL intentaría convertir los valores automáticamente `(123 -> '123')`

