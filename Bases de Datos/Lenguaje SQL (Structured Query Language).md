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



# Tipos de Datos en SQL

## Texto

### `VARCHAR`
- **Definición**: Tipo de dato para almacenar cadenas de texto de longitud variable. Se especifica un tamaño máximo `n` y la longitud real de la cadena se ajusta al contenido almacenado.
- **Formato típico**: `VARCHAR(n)` (e.g., `VARCHAR(100)`).

### `CHAR`
- **Definición**: Tipo de dato para almacenar cadenas de texto de longitud fija. Si la cadena almacenada es menor que el tamaño especificado, se rellena con espacios.
- **Formato típico**: `CHAR(n)` (e.g., `CHAR(10)`).

### `TEXT`
- **Definición**: Tipo de dato para almacenar cadenas de texto de longitud variable y potencialmente muy larga. A diferencia de `VARCHAR(n)`, no tiene un límite de longitud predefinido.
- **Formato típico**: `TEXT` 


## Numérico
### `INTEGER`
- **Definición**: Tipo de dato para almacenar números enteros, sin decimales. (4 bytes)
- **Formato típico**: `INTEGER` (e.g., `123`, `-456`).


### `SMALLINT`
- **Definición**: Tipo de dato para almacenar números enteros más pequeños. Ocupa menos espacio que `INTEGER`. (2 bytes)
- **Formato típico**: `SMALLINT` (e.g., `1000`, `-500`).

### `BIGINT`
- **Definición**: Tipo de dato para almacenar números enteros grandes. Útil para valores que superan el rango de `INTEGER`. (8 bytes)
- **Formato típico**: `BIGINT` (e.g., `123456789012345`, `-987654321`).

### `DECIMAL`
- **Definición**: Tipo de dato que almacena números con una precisión exacta y permite definir el número total de dígitos (`p`) y la cantidad de decimales (`s`).
- **Formato típico**: `DECIMAL(p, s)` (e.g., `DECIMAL(10, 2)` para valores como `12345.67`).

### `NUMERIC`
- **Definición**: Tipo de dato sinónimo de `DECIMAL` y con la misma funcionalidad. Ambos se utilizan para almacenar números con precisión exacta y permiten especificar la cantidad de dígitos y decimales.
- **Formato típico**: `NUMERIC(p, s)` (e.g., `NUMERIC(12, 4)` para valores como `123456.7890`).


### `FLOAT`
- **Definición**: Tipo de dato que almacena números en punto flotante. Permite representar números con un rango amplio pero con una precisión variable, lo que puede llevar a errores de redondeo.
- **Formato típico**: `FLOAT` (e.g., `FLOAT` o `FLOAT(53)` para una mayor precisión).


### `REAL`
- **Definición**: Tipo de dato de punto flotante similar a `FLOAT`, pero con una precisión menor. Generalmente, ocupa menos espacio y es menos preciso que `FLOAT`.
- **Formato típico**: `REAL` (e.g., `12345.6789`).


## Fecha y hora
### `TIMESTAMP`
- **Definición**: El tipo de dato `TIMESTAMP` se usa para almacenar fechas y horas completas, incluyendo la información de año, mes, día, hora, minuto, segundo y, en algunos casos, fracciones de segundo.
- **Formato típico**: `YYYY-MM-DD HH:MM:SS` (e.g., `2024-11-12 14:30:00`)

### `DATE`
- **Definición**: El tipo de dato `DATE` solo almacena la parte de la fecha (año, mes y día), sin incluir la hora.
- **Formato típico**: `YYYY-MM-DD` (e.g., `2024-11-12`)

### `TIME`
- **Definición**: Tipo de dato que almacena solo la parte de la hora, sin la fecha.
- **Formato típico**: `TIME` (e.g., `14:30:00`).


# Características
- Opera sobre un conjunto de tuplas
- No elimina automáticamente tuplas repetidas
- Es un lenguaje no procedural
- Su poder de expresión incluye el [[Algebra Relacional|álgebra relacional]] y lo extiende.

Se distinguen dos sub lenguajes
- DDL (Data definition Language)
- DML (Data Manipulation Language)


# [[Bases de Datos/Introducción#Lenguajes de base de datos#Data-Definition Language (DDL)|DDL]] (Data Definition Language)

Existen cuatro operaciones básicas: **CREATE**, **ALTER**, **DROP** y **TRUNCATE**.
Permite crear, modificar y eliminar objetos de la base de datos:
- Tablas
- Vistas, es una tabla virtual en el resultado de una consulta. Pueden usarse en consultas como si fueran tablas.
- Usuarios

## Crear una base de datos
Usamos

```sql
CREATE DATABASE <database_name>
```


## Operaciones sobre tablas

### ``CREATE TABLE``
Crea una nueva tabla

```sql
CREATE TABLE personas (
	cod INTEGER,
	apellidos VARCHAR(30),
	nombres VARCHAR(30)
)
```


### ``ALTER TABLE``
Modifica una tabla existente.

Si queremos agregar la columna `edad` a la tabla `personas` en **PostgreSQL**

```postgresql
ALTER TABLE personas ADD COLUMN edad SMALLINT;
```

### ``DROP TABLE``
Elimina una tabla existente y los datos almacenados en ella

Si queremos eliminar la tabla `personas`
```sql
DROP TABLE personas
```


# [[Bases de Datos/Introducción#Lenguajes de base de datos#Data-Manipulation Language (DML)|DML]] (Data Manipulation Language)

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
```

Ejemplo: 
```PostgreSQL
DELETE hospitales WHERE nomHosp = 'Loayza';
```

### ``UPDATE``
Actualiza tuplas de una tabla.
```sql
UPDATE nombre_tabla
SET columna1 = valor1, columna2 = valor2 ...
WHERE condicion;

```

```PostgreSQL
UPDATE hospitales 
SET direccion = '2 de Mayo'
WHERE codHosp = 1;
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

Se permiten los operadores `AND`, `OR` y `NOT` en la calificación de una consulta.

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

>[!tip] Nota
 SQL no es sensible a mayúsculas

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

```sql
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
FROM tabla;
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


---

# Uniones de tablas
Las uniones SQL se utilizan cuando queremos seleccionar datos de dos o más tablas.
Existen uniones al estilo **NO ANSI** (unión con `WHERE`) y uniones al estilo **ANSI** (con  JOIN)


### Tablas de Ejemplo

Para ilustrar los diferentes tipos de `JOIN`, utilizaremos tres tablas: **`empleados`**, **`departamentos`** y **`proyectos`**. A continuación se muestra la representación visual de cada una.

Tabla: `empleados`

| empleado\_id | nombre | apellido | departamento\_id | proyecto\_id |
| :---: | :---: | :---: | :---: | :---: |
| 1 | Ana | Gomez | 1 | 101 |
| 2 | Luis | Perez | 2 | 102 |
| 3 | Marta | Lopez | 1 | 103 |
| 4 | Pedro | Ramirez | 3 | 104 |
| 5 | Sofia | Torres | 4 | NULL |
| 6 | Carlos | Ruiz | NULL | 101 |

Tabla: `departamentos`

| departamento\_id | nombre\_departamento |
| :---: | :---: |
| 1 | Ventas |
| 2 | Marketing |
| 3 | Recursos Humanos |
| 5 | Investigacion |

Tabla: `proyectos`

| proyecto\_id | nombre\_proyecto | presupuesto |
| :---: | :---: | :---: |
| 101 | Proyecto Alpha | 50000.00 |
| 102 | Proyecto Beta | 75000.00 |
| 103 | Proyecto Gamma | 25000.00 |
| 105 | Proyecto Delta | 90000.00 |

### `INNER JOIN`

Un `INNER JOIN` retorna solo las filas que tienen valores coincidentes en ambas tablas. Es el tipo de `JOIN` más común.

```sql
SELECT columnas
FROM tabla1
INNER JOIN tabla2 ON tabla1.columna_comun = tabla2.columna_comun;
```

**Ejemplo**

Obtener los nombres de los empleados y el departamento al que pertenecen. ([[#Tablas de Ejemplo]])

```sql
SELECT
    e.nombre,
    e.apellido,
    d.nombre_departamento
FROM
    empleados AS e
INNER JOIN
    departamentos AS d ON e.departamento_id = d.departamento_id;
```

Salida

| nombre | apellido | nombre\_departamento |
| :---: | :---: | :---: |
| Ana | Gomez | Ventas |
| Luis | Perez | Marketing |
| Marta | Lopez | Ventas |
| Pedro | Ramirez | Recursos Humanos |



### `LEFT JOIN` (o `LEFT OUTER JOIN`)

[[Algebra Relacional#The left outer join (⟕)|Profundizar más]]
Un `LEFT JOIN` retorna todas las filas de la tabla izquierda (`empleados`) y las filas coincidentes de la tabla derecha (`departamentos`). Si no hay coincidencia, los valores de la tabla derecha serán **`NULL`**.

```sql
SELECT columnas
FROM tabla1
LEFT JOIN tabla2 ON tabla1.columna_comun = tabla2.columna_comun;
```

**Ejemplo**
Obtener todos los empleados y, si tienen, el nombre de su departamento. ([[#Tablas de Ejemplo]])

```sql
SELECT
    e.nombre,
    e.apellido,
    d.nombre_departamento
FROM
    empleados AS e
LEFT JOIN
    departamentos AS d ON e.departamento_id = d.departamento_id;
```

Salida

| nombre | apellido | nombre\_departamento |
| :---: | :---: | :---: |
| Ana | Gomez | Ventas |
| Luis | Perez | Marketing |
| Marta | Lopez | Ventas |
| Pedro | Ramirez | Recursos Humanos |
| Sofia | Torres | NULL |
| Carlos | Ruiz | NULL |

-----

### `RIGHT JOIN` (o `RIGHT OUTER JOIN`)

[[Algebra Relacional#The right outer join (⟖)| Profundizar más]]

Un `RIGHT JOIN` retorna todas las filas de la tabla derecha (`departamentos`) y las filas coincidentes de la tabla izquierda (`empleados`). Si no hay coincidencia, los valores de la tabla izquierda serán **`NULL`**.


```sql
SELECT columnas
FROM tabla1
RIGHT JOIN tabla2 ON tabla1.columna_comun = tabla2.columna_comun;
```

**Ejemplo**

Obtener todos los departamentos y los empleados que pertenecen a ellos. ([[#Tablas de Ejemplo]])


```sql
SELECT
    e.nombre,
    e.apellido,
    d.nombre_departamento
FROM
    empleados AS e
RIGHT JOIN
    departamentos AS d ON e.departamento_id = d.departamento_id;
```

Salida

| nombre | apellido | nombre\_departamento |
| :---: | :---: | :---: |
| Ana | Gomez | Ventas |
| Luis | Perez | Marketing |
| Marta | Lopez | Ventas |
| Pedro | Ramirez | Recursos Humanos |
| NULL | NULL | Investigacion |

### `FULL OUTER JOIN` 

[[Algebra Relacional#Full outer join (⟗)|Profundizar más]]

Un `FULL OUTER JOIN` retorna todas las filas de ambas tablas, combinando las coincidencias. Si una fila no tiene coincidencia en la otra tabla, las columnas de esa tabla serán **`NULL`**.


```sql
SELECT columnas
FROM tabla1
FULL OUTER JOIN tabla2 ON tabla1.columna_comun = tabla2.columna_comun;
```

**Ejemplo**

Obtener todos los empleados y todos los departamentos, mostrando las coincidencias y los que no tienen. ([[#Tablas de Ejemplo]])

```sql
SELECT
    e.nombre,
    e.apellido,
    d.nombre_departamento
FROM
    empleados AS e
FULL OUTER JOIN
    departamentos AS d ON e.departamento_id = d.departamento_id;
```

Salida

| nombre | apellido | nombre\_departamento |
| :---: | :---: | :---: |
| Ana | Gomez | Ventas |
| Luis | Perez | Marketing |
| Marta | Lopez | Ventas |
| Pedro | Ramirez | Recursos Humanos |
| Sofia | Torres | NULL |
| Carlos | Ruiz | NULL |
| NULL | NULL | Investigacion |

### `CROSS JOIN`

Un `CROSS JOIN` retorna el producto cartesiano de las filas de ambas tablas. Es decir, cada fila de la primera tabla se combina con cada fila de la segunda. No se utiliza una cláusula `ON` para este tipo de `JOIN`.


```sql
SELECT columnas
FROM tabla1
CROSS JOIN tabla2;
```

**Ejemplo**

Combinar cada empleado con cada proyecto. Esto puede generar una tabla muy grande, por lo que su uso es menos común. ([[#Tablas de Ejemplo]])

```sql
SELECT
    e.nombre,
    p.nombre_proyecto
FROM
    empleados AS e
CROSS JOIN
    proyectos AS p
LIMIT 5;
```

Salida (Ejemplo Parcial)

| nombre | nombre\_proyecto |
| :----: | :--------------: |
|  Ana   |  Proyecto Alpha  |
|  Ana   |  Proyecto Beta   |
|  Ana   |  Proyecto Gamma  |
|  Ana   |  Proyecto Delta  |
|  Luis  |  Proyecto Alpha  |

### `NATURAL JOIN`

Un `NATURAL JOIN` realiza una unión implícita basada en las columnas que tienen el **mismo nombre y tipo de dato** en ambas tablas. No necesitas especificar la cláusula `ON`, ya que el motor de la base de datos lo hace automáticamente. 

```sql
SELECT columnas
FROM tabla1
NATURAL JOIN tabla2;
```

**Ejemplo**

Obtener los empleados y su departamento. El `NATURAL JOIN` se realizará por la columna `departamento_id` que es común a ambas tablas. ([[#Tablas de Ejemplo]])

```sql
SELECT
    e.nombre,
    e.apellido,
    d.nombre_departamento
FROM
    empleados AS e
NATURAL JOIN
    departamentos AS d;
```

Salida

| nombre | apellido | nombre\_departamento |
| :---: | :---: | :---: |
| Ana | Gomez | Ventas |
| Luis | Perez | Marketing |
| Marta | Lopez | Ventas |
| Pedro | Ramirez | Recursos Humanos |

### `SELF JOIN`

Un `SELF JOIN` une una tabla consigo misma. Esto es útil para comparar filas dentro de la misma tabla. Para evitar conflictos, es crucial usar **alias de tabla** para diferenciar las dos instancias de la tabla.

```sql
SELECT columnas
FROM tabla1 AS T1
JOIN tabla1 AS T2 ON T1.columna = T2.columna;
```

**Ejemplo**

Suponiendo que un jefe de proyecto (`empleado_id`) es también un empleado, podemos encontrar empleados que trabajan en el mismo proyecto que 'Ana Gomez'. ([[#Tablas de Ejemplo]])

```sql
SELECT
    T1.nombre AS empleado,
    T2.nombre AS compañero_de_proyecto
FROM
    empleados AS T1
JOIN
    empleados AS T2 ON T1.proyecto_id = T2.proyecto_id
WHERE
    T1.nombre = 'Ana' AND T1.empleado_id <> T2.empleado_id;
```

Salida

| empleado | compañero\_de\_proyecto |
| :------: | :---------------------: |
|   Ana    |         Carlos          |

---


# Eliminar una columna de una tabla

```postgresql
alter table nombre_tabla drop column nombre_campo;
```


# Cambiar tipo de dato en una columna de una tabla vacía

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



---

# Operadores de agregación

Los operadores de agregación son funciones que toman una colección de valores como entrada y retornan un valor simple.

**Comportamiento de un Operador de Agregación**
- **Opera** en una sola columna 
- **Retorna** un solo valor. 
- Usado solo en la lista `SELECT` y en la cláusula `HAVING`.
- Acepta
	- ``DISTINCT``, considera solo valores distintos del argumento de la expresión.
	- ``ALL``, considera todos los valores incluyendo todos los duplicados.

Ejemplo:

```SQL
select count(distinct nombre_columna);
```


## Tipos de operadores de agregación
- ``SUM`` y ``AVG``: opera solo en una colección de números.
- ``MIN``, ``MAX`` y ``COUNT``: opera sobre una colección de tipos de datos numéricos y no numéricos.

Cada función **elimina** valores *NULL* y opera sobre valores *No-NULL*.

### Tabla ``empleado``

| numEmp | nombre | apellido | salario  | posicion           |
| ------ | ------ | -------- | -------- | ------------------ |
| SL100  | John   | White    | 30000.00 | Administrador      |
| SL101  | Susan  | Brand    | 24000.00 | Administrador      |
| SL102  | David  | Ford     | 12000.00 | Gestor de Proyecto |
| SL103  | Ann    | Beech    | 12000.00 | Gestor de Proyecto |
| SL104  | Mary   | Howe     | 9000.00  | Gestor de Proyecto |

### ``SUM()``
Retorna la suma de los valores en una columna específica.
**Ejemplo:** Recupere la suma total de los salarios de Administradores [[#Tabla ``empleado``|empleado]]
```sql
select sum(salario) as sum_salario
from empleado
where empleado.posicion = 'Administrador';
```

| sum_salario |
| ----------- |
| 54000.00    |

### `AVG()`
Retorna el promedio de los valores en una column especifica.
**Ejemplo:** Obtenga el promedio del salario de los gestores del proyecto. [[#Tabla ``empleado``|empleado]]
```sql
select avg(distinct salario) as media_salario
from empleado
where empleado.posicion='Gestor del Proyecto';
```

| media_salario |
| ------------- |
| 10500.00      |
**Al usar ``distinct`` no se toman en cuenta los salarios duplicados**


### ``MIN()``  y ``MAX()``
Retorna el valor más pequeño y más grande de una columna.
**Ejemplo:** Obtenga el salario mínimo y máximo de los empleados. [[#Tabla ``empleado``|empleado]]
```sql
select min(salario) as salario_min, max(salario) as salario_max
from empleado;
```

| salario_min | salario_max |
| ----------- | ----------- |
| 9000.00     | 30000.00    |
### ``COUNT()``
Retorna el numero de valores en la columna especificada
**Ejemplo:** Contabilice el numero de empleados que son Administradores [[#Tabla ``empleado``|empleado]]

```sql
select count(numEmp) as cuenta_numEmp
from empleado
where empleado.posicion='Administrador';
```

| cuenta_numEmp |
| ------------- |
| 2             |

### Uso de COUNT() y SUM()
**Ejemplo:** Halla el número total de Administrador y la suma de sus salarios. [[#Tabla ``empleado``|empleado]]
```sql
select count(numEmp) as cont_emp, sum(salario) as suma_salario
from empleado
where empleado.posicion='Administrador';
```

| cont_emp | suma_salario |
| -------- | ------------ |
| 2        | 54000.00     |

## ``COUNT(*)``
No hay entrada para esta función. Retorna todas las filas de una tabla, independientemente de si se producen valores nulos o duplicados. [[#Tabla ``empleado``|empleado]]

**Ejemplo:** ¿Cuántos Gestores de Proyecto tienen salario superior a 9000.00?
```sql
select count(*) as cuenta_salarioGP
from empleado.posicion='Gestor de Proyecto' and empleado.salario > 9000.00
```

| cuenta_salarioGP |
| ---------------- |
| 2                |

## Uso de operadores de agregación

### Tabla ``empleado``

| area | numEmp | nombre | apellido | salario  | posicion           |
| ---- | ------ | ------ | -------- | -------- | ------------------ |
| B3   | SL100  | John   | White    | 30000.00 | Administrador      |
| B5   | SL101  | Susan  | Brand    | 24000.00 | Administrador      |
| B3   | SL102  | David  | Ford     | 12000.00 | Gestor de Proyecto |
| B5   | SL103  | Ann    | Beech    | 12000.00 | Gestor de Proyecto |
| B7   | SL104  | Mary   | Howe     | 9000.00  | Gestor de Proyecto |

### GROUP BY
Agrupa los datos de la tabla en una consulta `select` y produce una única fila de resumen para cada grupo.

**Cuando usar `GROUP BY`**:
1. Cada elemento de la lista `SELECT` debe tener un solo valor por grupo.
2. La cláusula `SELECT` solo puede contener:
	- Nombres de Columnas
	- Operador de Agregación
	- Constante
	- Una expresión que contiene combinaciones de las anteriores
3. Todos los nombres de columna en la lista `SELECT` deben aparecer en la cláusula `GROUP BY` a menos que el nombre se use sólo en la función agregada.

**Ejemplo:** Encuentre el número de empleados que trabajan en cada área y la suman de sus salarios. [[#Uso de operadores de agregación#Tabla ``empleado``|empleado]] 
```sql
select area, count(numEmp) as cuenta, sum(salario) as suma
from empleado
group by area
order by area;
```

| area | cuenta | suma     |
| ---- | ------ | -------- |
| B3   | 2      | 42000.00 |
| B5   | 2      | 36000.00 |
| B7   | 1      | 9000.00  |

### HAVING
Esta diseñada para ser usada con `GROUP BY` de tal forma que puedan restringir los grupos que aparecen en la tabla resultado final.

**Ejemplo:** Para cada área con más de un empleado, hallar la cantidad de empleados que trabajan en cada área así como la suma de sus salarios. [[#Uso de operadores de agregación#Tabla ``empleado``|empleado]] 

```sql
select area, count(numEmp) as cuenta, sum(salario) as suma
from empleado
group by area
having count(numEmp) > 1
order by area;
```

Tabla resultado después de realizar la cláusula `GROUP BY` area.

| area | count | sum      |
| ---- | ----- | -------- |
| B3   | 2     | 42000.00 |
| B5   | 2     | 36000.00 |
| B7   | 1     | 9000.00  |

Tabla resultado final luego de realizar `HAVING COUNT(numEmp) > 1 ORDER BY area;`

| area | count | sum      |
| ---- | ----- | -------- |
| B3   | 2     | 42000.00 |
| B5   | 2     | 36000.00 |


