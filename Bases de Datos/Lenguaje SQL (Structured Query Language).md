El Lenguaje SQL es un lenguaje declarativo de acceso a bases de datos relacionales que permite especificar diversos tipos de operaciones sobre las mismas.
Reúne características del álgebra y el cálculo relacional permitiendo lanzar consultas con el fin de recuperar información de interés de una base de datos, de una forma sencilla.

# Orígenes

| Orígenes                                                                                                                 | Año  |
| ------------------------------------------------------------------------------------------------------------------------ | ---- |
| Edgard Codd propone el modelo relacional                                                                                 | 1970 |
| Basándose en las ideas de Codd IBM diseña SEQUEL y el SGBD System R                                                      | 1977 |
| Oracle introduce SEQUEL a nivel comercial                                                                                | 1979 |
| ANSI estandariza SQL (SQL-86 o SQL1), una versión extendida de SEQUEL                                                    | 1986 |
| Se lanza un nuevo estándar llamado SQL-92 o SQL2                                                                         | 1992 |
| Se agregaron expresiones regulares, consultas recursivas, triggers y algunas características orientadas a objetos (SQL3) | 1999 |
| Se introducen algunas características de XML, y otras funcionalidades                                                    | 2003 |

# Características
- Opera sobre un conjunto de tuplas
- No elimina automáticamente tuplas repetidas
- Es un lenguaje no procedural
- Su poder de expresión incluye el [[Algebra Relacional|álgebra relacional]] y lo extiende.

Se distinguen dos sub lenguajes
## [[Bases de Datos/Introducción#Lenguajes de base de datos#Data-Definition Language (DDL)|DDL]] (Data Definition Language)
Existen cuatro operaciones básicas: **CREATE**, **ALTER**, **DROP** y **TRUNCATE**.
Permite crear, modificar y eliminar objetos de la base de datos:
- Tablas
- Vistas, es una tabla virtual en el resultado de una consulta. Pueden usarse en consultas como si fueran tablas.
- Usuarios

### CREATE DATABASE
Usado para crear una base de datos
$$ \text{CREATE \: DATABASE \: nombre\_base\_datos }$$

### Operaciones sobre tablas

#### ``CREATE TABLE``
Crea una nueva tabla

```sql
create table personas (
	cod integer,
	apellidos varchar(30),
	nombres varchar(30)
)
```


#### ``ALTER TABLE``
Modifica una tabla existente

#### ``DROP TABLE``
Elimina una tabla existente y los datos almacenados en ella

```sql
drop table personas
```

## [[Bases de Datos/Introducción#Lenguajes de base de datos#Data-Manipulation Language (DML)|DML]] (Data Manipulation Language)
Existen cuatro operaciones básicas: **``INSERT``**, **``UPDATE``**, **``DELETE``** y **``SELECT``**

### ``INSERT``
Agrega tuplas a una tabla.
```sql
INSERT INTO nombre_tabla VALUES (valor1, valor2, ...);
INSERT INTO hospitales VALUES (1, '2 de Mayo', '2 de Mayo 1234');
```

### ``DELETE``
Elimina tuplas de una tabla que cumplan una condición.
```sql
DELETE FROM nombre_tabla
WHERE codicion;

DELETE hospitales WHERE nomHosp = 'Loayza';
```

### ``UPDATE``
Actualiza tuplas de una tabla.
```sql
UPDATE nombre_tabla
SET columna1 = valor1, columna2 = valor2 ...
WHERE condicion;

UPDATE hospitales SET direccion = '2 de Mayo'
WHERE codHosp = 1
```


### Clausula ``SELECT``
La instrucción ``SELECT`` se utiliza para recuperar informaciones de una o más tablas.
La estructura básica de ``SELECT`` esta compuesta de tres partes principales:
1. Lista de las columnas a ser recuperadas.
2. Lista de las tablas a ser consultadas.
3. Restricciones (opcional)
Tambien soporta las siguientes clausulas opcionales: **WHERE**, **GROUP BY**, **HAVING**, **ORDER BY**

La clausula ``SELECT`` puede:
- Listar todas las columnas de una tabla
```sql
	SELECT * FROM nombre_tabla;
```

- Listas columnas específicas de una tabla

```sql
	SELECT nombre_atributo1, nombre_atributo2, ...
	FROM nombre_tabla;
```

- Ejecutar operaciones entre columnas listadas
```sql
	SELECT matricula, (nota1, nota2 + nota3)/3
	FROM notas;
```

- Ejecutar operaciones aritméticas
```sql
	SELECT 3*4;
```

- Llamar a funciones nativas o programadas por el usuario
```sql
	SELECT random();
```

- Aplicar funciones sobre las columnas listadas
```sql
	SELECT substr(nombre, 1, 4)
	FROM persona;
	
	SELECT length(nombre)
	FROM persona;
```

- Podemos alterar el nombre de una columna mostrada en la salida a través del uso de alias

```sql
SELECT matricula, (nota1 + nota2 + nota3)/3 AS media
FROM notas;
```

| matricula | media            |
| --------- | ---------------- |
| 20100417G | 13.6666666666667 |
| 20110751J | 13.6666666666667 |
| 20129187T | 13.3333333333333 |

- Se puede eliminar resultados duplicados, en la salida, usando la palabra reservada DISTINCT

### Cláusula ``FROM``
Indica el origen de los datos de una consulta, que pueden ser
- Una tabla
- Dos o más tablas (Joined Tables)
- Subconsultas
- Vistas

### Cláusula ``WHERE``
Después de ser procesada por la cláusula FROM, cada fila de la tabla virtual derivada es verificada en la condición de búsqueda.

Se permiten los operadores **AND**, **OR** y **NOT** en la calificación de una consulta.

```sql
select model, manufacture_year, color, value
from automovil
where model='GOL' and manufacture_year<2005;
```


| Operador     | Descripción                                                                           |
| ------------ | ------------------------------------------------------------------------------------- |
| >, <, >=, <= | Mayor que, Menor que, Mayor igual que, Menor igual que                                |
| =, <>        | Igual, Diferente                                                                      |
| BETWEEN      | Entre un rango inclusivo                                                              |
| LIKE         | Búsqueda de un patron. Usa comodines                                                  |
| IN           | Si se conoce el valor exacto que se quiere retornar para al menos una de las columnas |


### Recuperación de datos
```sql
SELECT A1, ..., An
FROM R1, ..., Rm
WHERE C;
```
- $A_1, \cdots, A_n$ son los nombres de atributos, también se puede utilizar (\*).
- $R_1, \cdots, R_m$ son los nombres de las tablas.
- $C$ es una condición booleana.

**SQL no es sensible a mayúsculas**

### Clausula ``ORDER BY``
Permite ordenar el resultado ascendentemente o descendentemente. Se usa para ordenar el conjunto resultado por una columna específica. De forma predeterminada ordena los registros de forma ascendente.

```sql
SELECT columnas
FROM tablas
ORDER BY nombre_columna(s) ASC|DESC;
```

### Clausula ``DISTINCT``
Permite filtrar tuplas repetidas

```sql
SELECT DISTINC columnas
FROM tablas
```

### Clausula ``LIMIT``
Usada para especificar el número de registros a devolver.
```
SELECT columnas
FROM tablas
LIMIT numero
```

### Comodines SQL
Pueden sustituir uno o más caracteres cuando se buscan datos en una base de datos.
Los comodines SQL deben ser usados con el operador LIKE.
- $\%$ sustituye a cero o más caracteres
- $\_$ sustituye exactamente a un caracter

**Ejemplo**

```sql
SELECT * FROM personas
WHERE distrito LIKE 'SA%';
```

| cod | apellidos         | nombres | dni      | ecivil  | domicilio                 | distrito   |
| --- | ----------------- | ------- | -------- | ------- | ------------------------- | ---------- |
| 4   | CALLE ORBEGOZO    | CECILIA | 25879635 | Soltera | CALLE PERUANIDAD 1265     | SAN MARTIN |
| 10  | EIZAGUIRRE ZAPATA | ROSA    | 69459876 | Casada  | CALLE LAS FLORESTAS 721   | SALAMANCA  |
| 20  | JUSTO SOTO        | JULIA   | 69149994 | Soltera | AV JAVIER PRADO OESTE 199 | SAN ISIDRO |


```sql
SELECT * FROM personas
WHERE distrito LIKE '%NC%';
```

| cod | apellidos         | nombres   | dni      | ecivil  | domicilio               | distrito  |
| --- | ----------------- | --------- | -------- | ------- | ----------------------- | --------- |
| 10  | EIZAGUIRRE ZAPATA | ROSA      | 69459876 | Casada  | CALLE LAS FLORESTAS 721 | SALAMANCA |
| 13  | GIRON ESPINOZA    | GERARDINA | 59366911 | Soltera | AV PUERTO CHICO S6      | BARRANCO  |
| 17  | JARAMILLO ACERO   | LUISA     | 29242959 | Casada  | AV JORGE CHAVEZ H 9     | BARRANCO  |


```sql
SELECT * FROM personas
WHERE nombres LIKE '_LI';
```

| cod | apellidos          | nombres | dni      | ecivil  | domicilio          | distrito  |
| --- | ------------------ | ------- | -------- | ------- | ------------------ | --------- |
| 11  | FELICIANO FIGUEROA | ELI     | 49428888 | Soltera | CALLE LA MURZA 621 | LA MOLINA |


```sql
SELECT * FROM personas
WHERE nombres LIKE 'G_ET_EL';
```

| cod | apellidos          | nombres | dni      | ecivil | domicilio               | distrito |
| --- | ------------------ | ------- | -------- | ------ | ----------------------- | -------- |
| 15  | SEGOVIA BARRIENTOS | GRETHEL | 69304935 | Casada | AV CAMINOS DEL INCA 821 | SURCO    |

### Operador ``IN``
Se usa para especificar múltiples valores en una cláusula WHERE.

```sql
SELECT columnas
FROM tabla
WHERE columna IN (valor1, valor2, ...);
```

**Ejemplo**

```sql
SELECT * FROM personas
WHERE nombres in ('MARIA', 'LUISA');
```

| cod | apellidos       | nombres | dni      | ecivil  | domicilio                | distrito   |
| --- | --------------- | ------- | -------- | ------- | ------------------------ | ---------- |
| 8   | DURAN PALACIOS  | MARIA   | 19521852 | Soltera | CALLE EL SOL H7          | CHORRILLOS |
| 12  | FARFAN ATOCHE   | LUISA   | 25310307 | Soltera | CALLE JULIO C. TELLO 120 | CALLAO     |
| 17  | JARAMILLO ACERO | LUISA   | 29242959 | Casada  | AV JORGE CHAVEZ H 9      | BARRANCO   |
| 18  | ORINA VARILLAS  | MARIA   | 99211970 | Casada  | AV EL NARANJAL 794       | LOS OLIVOS |


```sql
SELECT * FROM personas
WHERE nombres in 
(SELECT nombres FROM personas WHERE distrito='SURCO');
```

| cod | apellidos          | nombres | dni      | ecivil  | domicilio               | distrito |
| --- | ------------------ | ------- | -------- | ------- | ----------------------- | -------- |
| 9   | LETONA CASANI      | DANNY   | 89490864 | Casada  | CALLE EL GOLF 661       | SURCO    |
| 14  | ALARCON LAMAS      | SONIA   | 89335923 | Soltera | AV TOMAS MARZANO 4993   | SURCO    |
| 15  | SEGOVIA BARRIENTOS | GRETHEL | 69304935 | Casada  | AV CAMINOS DEL INCA 821 | SURCO    |

### Operador ``BETWEEN``
Usado en una cláusula WHERE para seleccionar un rango de datos entre dos valores.
```sql
SELECT columnas
FROM tabla
WHERE columna BETWEEN valor1 AND valor2;
```


```sql
SELECT * FROM personas
WHERE nombres BETWEEN 'ANA' AND 'DANNY';
```

| cod | apellidos      | nombres     | dni      | ecivil  | domicilio             |
| --- | -------------- | ----------- | -------- | ------- | --------------------- |
| 4   | CALLE ORBEGOZO | CECILIA     | 25879635 | Soltera | CALLE PERUANIDAD 1265 |
| 5   | CRUZ DIAZ      | ANA CECILIA | 23697410 | Soltera | PAVAYACU 125 - CALLAO |
| 9   | LETONA CASANI  | DANNY       | 89490864 | Casada  | CALLE EL GOLF 661     |


```sql
SELECT * FROM personas
WHERE nombres 
NOT BETWEEN 'CECILIA' AND 'MARIA';
```

| cod | apellidos         | nombres      | dni      | ecivil  |
| --- | ----------------- | ------------ | -------- | ------- |
| 3   | CACERES GUTIERREZ | ADELAIDA     | 25469874 | Casada  |
| 5   | CRUZ DIAZ         | ANA CECILIA  | 23697410 | Soltera |
| 6   | CRUZ MENA         | SANDRA MARIA | 25987634 | Casada  |
| 10  | EIZAGUIRRE ZAPATA | ROSA         | 69459876 | Casada  |
| 14  | ALARCON LAMAS     | SONIA        | 89335923 | Soltera |


### Alias
Se puede asignar un alias a una tabla o una columna
```sql
SELECT columnas
FROM tabla AS alias;

--O tambien

SELECT columna AS alias
FrOM tabla;
```


```sql
select po.OrderID, p.Apellidos, p.FirstName
from Personas as p, Ordenes as po
where p.Apellidos='GUTIERREZ LUNA' and p.Nombres='IRIS';

--Sin alias
select Ordenes.OrderID, Personas.Apellidos, Personas.Nombres
from Personas, Ordenes
where Personas.Apellidos='GUTIERREZ LUNA' and Personas.Nombres='IRIS';
```



# Uniones de tablas
Las uniones SQL se utilizan cuando queremos seleccionar datos de dos o más tablas.
Existen uniones al estilo **NO ANSI** (unión con WHERE) y uniones al estilo ANSI (con  JOIN)


## CROSS JOIN
Devuelve un conjunto de informaciones que son el resultado de todas las combinaciones posibles entre los registros de las tablas consideradas.

## NATURAL JOIN
Realiza la unión tomando como base los atributos del mismo nombre en las tablas consideradas.

## INNER JOIN
Es la unión estándar. Puede ser escrita también usando solo JOIN. Devuelve las informaciones con tan solo las tuplas que cumplan las definiciones de esta relación.

## LEFT OUTER JOIN
Devuelve todas las tuplas de la tabla de la izquierda. [[Algebra Relacional#The left outer join (⟕)|Profundizar más]]
## RIGHT OUTER JOIN
Devuelve todas las tuplas de la tabla de la derecha [[Algebra Relacional#The right outer join (⟖)| Profundizar más]]

## FULL OUTER JOIN
Devuelve todas las tuplas de ambos lados [[Algebra Relacional#Full outer join (⟗)|Profundizar más]]

## SELF JOIN
Realiza una unión de una tabla consigo misma. Para evitar que se presenten conflictos se requiere usar los alias.


# Eliminar una columna de una tabla

```postgresql
alter table nombre_tabla drop column nombre_campo;
```


# Cambiar tipo de dato en una columna de una tabla vacia

```postgresql
ALTER TABLE pasajero 
ALTER COLUMN pais_residencia 
TYPE integer USING pais_residencia::integer;
```


# Cambiar el nombre de la columna de una tabla

```postgresql
ALTER TABLE nombre_de_la_tabla
RENAME COLUMN nombre_actual TO nuevo_nombre;
```

