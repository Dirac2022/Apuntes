
# Laboratorio 1 

## Introducción a PostgreSQL
Para instalar **PostgreSQL**
```bash
sudo apt update
sudo apt upgrade

sudo apt install postgresql
```

Para validar que **PostgreSQL** se haya instalado correctamente (en Ubuntu)
```bash
system status postgresql
```
Se escribe `q` para salir.

Para cambiar del usuario root al usuario postgres
```bash
sudo -i -u postgres
```

**Bases de datos predeterminadas**
- postgres
- template0
- template1
Usuario predeterminado: postgres

Ingresar al psql con el usuario postgres en la base de datos postgres (en Ubuntu)
```bash
sudo su
su postgres
psql -U postgres -d postgres
```


Para ver usuarios
```postgresql
\du
```


> [!important] Los comandos de creación o modificación deben terminar en punto y coma

Estando en root@..
Para iniciar postgres escribimos
```bash
sudo -i -u postgres
```
Con eso nos encontramos con el usuario predeterminado de postgres.

## Inicio de laboratorio

- Conexión a una base de datos con un usuario especificado
- Crear un usuario con contraseña y permiso para crear base de datos
- Eliminar un usuario
- Atajo para salir de psql
- Crear una base de datos
- Renombrar una base de datos
- Listar las bases de datos creadas
- Conectarse a una base de datos
- Eliminar una base de datos

1. Conectarse a la base de datos template1 con el usuario postgres
Estando en postgres@...: ~$
```bash
psql -U postgres -d template1
```
Ingresamos con el usuario postgres a la base de datos template1


2. Procede a crear el usuario YOICHI y asignarle el password '12345'
```postgresql
create user yoichi wih password '12345';
```

3. Crear el usuario PIERO otorgándole el permiso para crear bases de datos y estableciendo su contraseña a 'goldennumber'
```postgresql
create user piero with createdb password 'goldennumber';
```


4. ¿Qué atajo se usa para abandonar la sesión de psql?
```postgresql
\q
```

5. Conectarse ahora a la base de datos template1 con el usuario YOICHI
```postgresql
psql -U yoichi -d template 1
```

6. Crear la base de datos bdsimple. Explique lo sucedido
```postgresql
create database bdsimple;
```

>[!error] usuario yoichi no tiene permiso para crear una base de datos, por lo tanto nos sale un error

7. Conectarse a la base de datos template1 con el usuario PIERO
```postgresql
\q
psql -U piero -d template 1
```

8. Crear las bases de datos bdsimple, personal con el nuevo usuario
```postgresql
create database bdsimple;
create database personal;
```

9. ¿Qué atajo se usa para listar las bases de datos creadas?
```postgresql
\l
\list
```

10. Conectarse a la base de datos bdsimple
```postgresql
\c bdsimple
```

11. Conectarse a la base de datos personal
```postgresql
\c personal
```

12. Eliminar la base de datos personal. Comente lo sucedido
>[!error] No se puede eliminar la base de datos activa (personal)
```postgresql
\c
drop database personal;
```

13. Eliminar la base de datos bdsimple
```postgresql
drop database bdsimple;
```

14. Conectarse ahora a la base de datos template1 con el usuario postgres
```bash
\q
psql -U postgres -d template1
```

15. Procede a crear el usuario CYNTHIA asignándole el password 'qbit'
```postgresql
create user cynthia with password 'qbit';
```

16. Eliminar el usuario CYNTHIA
```postgresql
drop user cynthia;
```

17. Cambiar el nombre de la base de datos personal por rrhh
```postgresql
alter database personal rename to rrhh;
```

18. Conectarse ahora la base de datos rrhh
```postgresql
\c rrhh
```

19. Volver a renombrar la base de datos rrhh por personal. ¿Qué sucede?
>[!error] No se puede renombrar la base de datos que se este ejecutando actualmente
```postgresql
\c postgres
alter database rrhh rename to personal;
```



# Laboratorio 15 - 06/06/24

## MongoDB
Por supuesto, aquí tienes el texto sin los asteriscos:

Para instalación de mongoDB

https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/

Para acceder a mongo:
```
mongosh
```

Crear base de datos:
```
use nombre_bd
```

Un documento es un conjunto de objetos clave valor, como un diccionario en python,
o como los archivos JSON. Serian lo análogo a las tuplas o registros de
las tablas en bases de datos relacionales.

2. **Crear base de datos mibd:**
```
use mibd
```

3. **Muestre la base de datos actualmente en uso:**
```
db
```

4. **Ahora proceda a listar todas las bases de datos disponibles:**
```
show dbs
```

5. **Comando para eliminar la base de datos seleccionada actualmente**
```
db.dropDatabase()
```



Para eliminar una base de datos debemos estar en ella, si deseamos
borrar la bd ventas:
```
use ventas
db.dropDatabase()
```

Salir de la sesión:
```
exit()
```

6. **Crear la base de datos ventas**
```
use ventas
```

7. **Crear la coleccion productos**
```
db.createCollection("Productos")
```


8. **Utilice el método *insert* para crear la colección Pedidos**
```
db.Pedidos.insert([{"idepedido" : 100 , "cliente" : "Luis" , "fpedido" : "18/05/2024"}])
```

9. **Escriba el comando para mostrar todas las colecciones creadas hasta el momento**
```
show collections()
```


Eliminar una collection
```
db.NombreColeccion.drop()
```


10. **Proceda a eliminar la colección Productos**
```
db.Productos.drop()
```


Crear una coleccion:
```
db.createCollection("Clientes")
```


Insertar un documento (registro)
db.NombreColeccion.insertOne([{datos clave:valor}])

Insertar varios documentos
db.NombreColeccion.insertMany([{datos1 clave:valor}, ... , {datosn clave:valor}])



11. **Un documento en MongoDB es lo mismo que un registro en bases**
de datos. 

Primero creamos la coleccion Clientes:

```
db.createCollection("Clientes")
```

Para insertar varios registros, tomamos como ejemplo la tabla, el codigo es

```
db.Clientes.insertMany([
{"idcliente" : "C001", "nombre" : "RICK", "apellido" : "TAPIA", "edad" : 21}, 
{"idcliente" : "C002", "nombre" : "THALIA", "apellido" : "ARELLANO", "edad" : 22}, 
{"idcliente" : "C003", "nombre" : "ANTONIO", "apellido" : "QUINTANA", "edad" : 25}, 
{"idcliente" : "C004", "nombre" : "GUILLERMO", "apellido" : "SANCHEZ", "edad" : 39}, 
{"idcliente" : "C005", "nombre" : "JACKY", "apellido" : "SANCHEZ", "edad" : 43} 
])
```



pretty() nos da una visualización mas "estética" de los datos


12. **Obtener todos los documentos de la colección Clientes:**
```
db.Clientes.find().pretty()
```


Listar todos los documentos:
```
db.NombreColeccion.find()
```

Obtener el primer documento
```
db.NombreColeccion.findOne()
```


13. **Obtener el primero documento de la colección Clientes:**
```
db.Clientes.findOne()
```



14. **Recupere el documento que corresponde al cliente de código C002:**
```
db.Clientes.find({"idcliente" : "C002"}).pretty()
```


- $gt: greater than
- $gte: greater than or equal
- $lt: less than
- $lte: less than or equal
- $eq: equal
- $ne: not equal

15. *Recupere los documentos que corresponde a todos los clientes de edad mayor de 22:*
```
db.Clientes.find({"edad":{$gt:22}})
```

16. **Recupere los documentos que corresponden a todos los clientes de edad mayor o igual a 25**
```
db.Clientes.find({"edad":{$gte:25}})
```

17. **Recupere los documentos que corresponden a todos los clientes menores de 22 años**
```
db.Clientes.find({"edad":{$lt:22}})
```

18. **Recupere los documentos que corresponden a los clientes que no tengan 39 años**
```
db.Clientes.find({"edad" : {$ne:39}})
```

19. **Recupere los documentos que corresponden a los clientes de apellido SANCHEZ y edad 39 años**
```
db.Clientes.find({"edad" : {$eq:39}, "apellido" : "SANCHEZ"})
```
o también
```
db.Clientes.find({"edad" : 39, "apellido" : "SANCHEZ"})
```


20. **Recupere los dodumentos que corresponden a todos los clientes cuyo apellido es Sanchez o que tengan una edad de 25 años:**
```
db.Clientes.find({ $or:[ {"apellido" : "SANCHEZ"}, {"edad" : 25}]})
```


21. **Realice la búsqueda del quinto cliente mediante su clave *_id* y modifique su apellido por GARCIA:**
```
db.Clientes.update( {"_id":ObjectId("...")} , {$set:{"apellido":"GARCIA"}} )
```



En ObjectId("...") iria el ObjectId  del quinto cliente, por ejemplo:
```
db.Clientes.update( {"_id":ObjectId("6662545c2c1b282b4fa26a18")} , {$set:{"apellido":"GARCIA"}} )
```

El *ObjectId* se puede apreciar cuando usamos los comandos find() o find().pretty()

22. **Actualice al cliente que tiene 21 años modificando su nombre por STING:**
```
db.Clientes.update({"edad":21} , {$set:{"nombre":"STING"}})
```

Eliminar un documento:
```
db.NombreColeccion.remove(condicion)
```


23. **Elimine al cliente que tiene 25 años de edad**
```
db.Clientes.remove({"edad" : 25})
```

Sin embargo, este comando no es recomendable, se recomienda:
```
db.NombreColeccion.deleteMany(condicion)  // Si queremos eliminar muchos documentos
db.NombreColeccion.deleteOne(condicion)   // Si queremos solo eliminar uno, el primero
```

