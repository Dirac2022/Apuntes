https://es.slideshare.net/slideshow/networking-ii-mongodb-primeros-pasos/237981408

# Introducción

## Características

- Es una base de datos NoSQL orientada a documentos. El nombre viene derivado de "humongous" (enorme, extraordinariamente largo).
- Primera versión publicada en marzo de 2009: 0.9 publicada en código abierto bajo licencia AGPL.
- Primera versión estable publicada en agosto de 2009: 1.0.
- En 2011, se lanzó la version 1.4, la primera versión considerada como apta para su producción y distribución.
- MongoDB es una base de datos de documentos de código abierto y una base de datos NoSQL líder.
- MongoDB está escrito en C++.
- MongoDB trabaja en concepto de colección y documento.

## Comparación entre MongoDB y Sistemas de base de datos relacionales


| RDBMS                      | MongoDB                                                 |
| -------------------------- | ------------------------------------------------------- |
| Database                   | Database                                                |
| Table                      | Collection                                              |
| Tuple/Row                  | Document                                                |
| Column                     | Field                                                   |
| Table Join                 | Embedded Documents                                      |
| Primary Key                | Primary Key (Default key_id provided by mongodb itself) |

**Database Server and Client**

| Mysqld/Oracle | mongod |
| ------------- | ------ |
| mysql/sqlplus | mongo  |
![[esquema mongodb.png]]


## Documento
- Es un conjunto de pares clave-valor. Los documentos tienen un esquema dinámico.
- El esquema dinámico significa que los documentos en la misma colección no necesitan tener el mismo conjunto de campos o estructura, y los campos comunes en los documentos de una colección pueden contener diferentes tipos de datos.

## Colección
- Es un grupo de documentos MongoDB.
- Es el equivalente de una tabla RDBMS. Existe una colección dentro de una única base de datos.
- Los documentos dentro de una colección pueden tener diferentes campos.

## Campos
Campos de un documento a los que se les asigna valor y sobre los que se pueden crear índices. **Símil a las columnas en bases de datos relacionales**.

#### \_id:
Campo especial que identifica a cada documento en una colección. Si no se le da valor en el insertado, se genera automáticamente. **Siempre está presente en los documentos**.


## Documento en MongoDB

![[Pasted image 20240620182340.png]]

## Colección en MongoDB

![[Pasted image 20240620182546.png]]

## Modelo de Datos

- Las colecciones pueden crearse de la siguiente forma:
```mongodb
db.createCollection(name, options)
```

- Ejemplo de creación de colección:
```mongodb
db.createCollection("socios", {size: 2145678899, autoIndexId: true, ...})
```
Donde:
- *socios*: nombre de la colección
- *{size ...}*: opciones como tamaño, índice, etc.

En mongoDB las colecciones se crean automáticamente la primera vez que se hace referencia a ellas (por ejemplo, al insertar un primer documento), por lo que no es necesario utilizar "createCollection". Este es sólo necesario si se quieren modificar los valores por defecto de las opciones.


# Tipos de datos

## Numéricos

| Nombre  | Tipo          | Tamaño   |
| ------- | ------------- | -------- |
| Double  | coma flotante | 64 bits  |
| Decimal | coma flotante | 128 bits |
| Int     | entero        | 32 bits  |
| Long    | entero        | 64 bits  |

## Texto

| Nombre | Caracteristica                 |
| ------ | ------------------------------ |
| String | strings UTF-8                  |
| Regex  | Almacena expresiones regulares |

## Fecha

| Nombre    |        |         |                                                                  |
| --------- | ------ | ------- | ---------------------------------------------------------------- |
| Date      | entero | 64 bits | Representa el número de milisegundos desde el 1 de enero de 1970 |
| Timestamp | entero | 64 bits | En una instancia mongod, cada valor de timestamp es único        |

## Especiales

| Nombre     | Característica                                                                               |
| ---------- | -------------------------------------------------------------------------------------------- |
| Array      | Almacena un conjunto de elementos de cualquier tipo.                                         |
| ObjectId   | Tipo de dato único, principalmente utilizado para dar valor al campo \_id de los documentos. |
| Javascript | Código Javascript                                                                            |
| Null       | Valor nulo.                                                                                  |
| Boolean    | Valor booleano                                                                               |

# Consulta y modificación de datos
- Los datos son accedidos mediante operaciones *CRUD* (*create*, *read*, *update*, *delete*):
	- **Find**: lectura (read) de datos. Símil con el *select* en SQL.
	- **Insert**: escritura (create) de datos.
	- **Update**: actualización de valores en los datos.
	- **Remove**: borrado (delete) de datos.
- La ejecución de cualquiera de estas instrucciones sigue el siguiente esquema:
```mongodb
db.<nombre_coleccion>.<nombre_operacion>(<condiciones de la operacion>)
```

## Consultas: operación find
![[Pasted image 20240620190258.png]]
Los campos consultados pueden ir opcionalmente entre comillas simples o dobles. Las tres consultas que se muestran a continuación funcionan exactamente igual:
```mongodb
db.socios.find({numSocio : {$gt: 300}})
```

```mongodb
db.socios.find({'numSocio' : {$gt: 300}})
```

```mongodb
db.socios.find({"numSocio" : {$gt: 300}})
```

## Condiciones
Existen diferentes tipos de operaciones:

### Operaciones de comparación

#### De igualdad ($eq)

```mongodb
db.socios.find({numSocio : {$eq : 300}})
```
#### Mayor que ($gt)
```mongodb
db.socios.find({numSocio : {$gt : 300}})
```

#### Menor que ($lt)
```mongodb
db.socios.find({numSocio : {$lt : 300}})
```

#### Diferente a ($ne)
```mongodb
db.socios.find({numSocio : {$ne : 300}})
```

#### Mayor o igual que ($gte)
```mongodb
db.socios.find({numSocio : {$gte : 300}})
```

#### Menor o igual que ($lte)
```mongodb
db.socios.find({numSocio : {$lte : 300}})
```

#### Pertenece (\$in) o no (\$nin) a un conjunto
```mongodb
db.socios.find({numSocio : {$in : [300, 301]}})
```

```mongodb
db.socios.find({numSocio : {$nin : [300, 3001]}})
```


### Operadores lógicos

#### Ambas condiciones ha de cumplirse ($and)
```mongodb
db.socios.find({$and : [{nombre: "Juan"}, {apellido1: "Galindo"}]})
```


#### Alguna de las condiciones ha de cumplirse ($or)
```mongodb
db.socios.find({$or: [{nombre: "Juan"}, {apellido1: "Galindo"}]})
```

#### No debe de cumplir la condición ($not)
```mongodb
db.socios.find({numSocio: {$not: {$eq: 300}}})
```

#### Que no se cumpla ninguna condición ($nor)
```mongodb
db.socios.find({$nor : [{nombre: "Juan"}, {apellido1: "Galindo"}]})
```


### Proyecciones
- Valor 1 si queremos mostrar el campo.
- Valor 0 si no queremos mostrarlo.
- Por defecto, si no se declara nada en la proyección, se muestran todos los campos:
	- Al poner un campo a 1, se muestra solamente ese campo.
	- **El campo \_id se muestra siempre por defecto** aunque haya otros campos en la proyección con valor 1.
	- Si no se quiere mostrar el campo \_id, hay que ponerlo a 0 explícitamente en la proyección.

#### Ejemplos
Muestra *nombre*, *apellido1* y *\_id*
```mongodb
db.socios.find({numSocio: {$eq: 300}}, {nombre:1, apellido1:1})
```

Muestra *nombre* y *apellido1*
```mongodb
db.socios.find({numSocio: {$eq: 300}}, {nombre:1, apellido1:1, _id:0})
```

Muestra todos los campos excepto *numSocio*
```mongodb
db.socios.find({numSocio: {$eq: 300}}, {numSocio:0})
```


## Modificadores
### Sort
Ordena los resultados según los campos dados. Un valor de 1 indica ordenamiento ascendente, y un valor de -1 ordenamiento descendente.

```mongodb
db.socios.find({numSocio: {$eq: 300}}, {nombre:1, apellido1:1}).sort({nombre:1})
```

### Limit
Limita el número de colecciones retornadas. El 0 indica que no hay límite.
```mongodb
db.socios.find({numSocio: {$eq: 300}}, {nombre:1, apellido1:1}).limit(3)
```


## Operación
### Insert
```mongodb
db.socios.insert({numSocio:300, nombre:"Pablo", ...})
```
Si no se inserta un valor para el campo *\_id* se generará automáticamente:
- *\_id* único, no hay peligro de *UPSERTS*: si se inserta un valor existente en la colección, devuelve **error**.

>En MongoDB, un **upsert** es una operación que combina la funcionalidad de "update" (actualización) y "insert" (inserción). La operación upsert permite actualizar un documento si este ya existe, y si no existe, inserta un nuevo documento. Este comportamiento es especialmente útil cuando no se sabe de antemano si el documento ya está presente en la colección.


### Update
```mongodb
db.socios.update({numSocio:300}, {$set: {nombre:"Pablo"}} {multi:true})
```
- `{numSocio:300}` es la condición
- `{$set: {nombre: "Pablo"}}` es el nuevo valor
- `{multi: true}` es la opción.

La opción `multi:true` en la operación *update* indica que se pueden modificar varios documentos simultáneamente.

### Remove
```mongodb
db.socios.remove({numSocio: 300})
```
