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

#### CREATE TABLE
Crea una nueva tabla
![[Pasted image 20240502082024.png]]


#### ALTER TABLE
Modifica una tabla existente

#### DROP TABLE
Elimina una tabla existente y los datos almacenados en ella


## [[Bases de Datos/Introducción#Lenguajes de base de datos#Data-Manipulation Language (DML)|DML]] (Data Manipulation Language)
Existen cuatro operaciones básicas: **INSERT**, **UPDATE**, **DELETE** y **SELECT**

### INSERT
Agrega tuplas a una tabla.
```
INSERT INTO nombre_tabla VALUES (valor1, valor2, ...);
INSERT INTO hospitales VALUES (1, '2 de Mayo', '2 de Mayo 1234');
```

### DELETE
Elimina tuplas de una tabla que cumplan una condición.
```
DELETE FROM nombre_tabla
WHERE codicion;

DELETE hospitales WHERE nomHosp = 'Loayza';
```

### UPDATE
Actualiza tuplas de una tabla.
```
UPDATE nombre_tabla
SET columna1 = valor1, columna2 = valor2 ...
WHERE condicion;

UPDATE hospitales SET direccion = '2 de Mayo'
WHERE codHosp = 1
```


### Clausula SELECT
La instrucción SELECT se utiliza para recuperar informaciones de una o más tablas.
La estructura básica de SELECT esta compuesta de tres partes principales:
1. Lista de las columnas a ser recuperadas.
2. Lista de las tablas a ser consultadas.
3. Restricciones (opcional)
Tambien soporta las siguientes clausulas opcionales: **WHERE**, **GROUP BY**, **HAVING**, **ORDER BY**

La clausula SELECT puede:
- Listar todas las columnas de una tabla
```
	SELECT * FROM nombre_tabla;
```

- Listas columnas específicas de una tabla

```
	SELECT nombre_atributo1, nombre_atributo2, ...
	FROM nombre_tabla;
```

- Ejecutar operaciones entre columnas listadas
```
	SELECT matricula, (nota1, nota2 + nota3)/3
	FROM notas;
```

- Ejecutar operaciones aritméticas
```
	SELECT 3*4;
```

- Llamar a funciones nativas o programadas por el usuario
```
	SELECT random();
```

- Aplicar funciones sobre las columnas listadas
```
	SELECT substr(nombre, 1, 4)
	FROM persona;
	
	SELECT length(nombre)
	FROM persona;
```

- Podemos alterar el nombre de una columna mostrada en la salida a través del uso de alias
![[Pasted image 20240502102048.png]]

- Se puede eliminar resultados duplicados, en la salida, usando la palabra reservada DISTINCT

### Cláusula FROM
Indica el origen de los datos de una consulta, que pueden ser
- Una tabla
- Dos o más tablas (Joined Tables)
- Subconsultas
- Vistas

### Cláusula WHERE
Después de ser procesada por la cláusula FROM, cada fila de la tabla virtual derivada es verificada en la condición de búsqueda.

Se permiten los operadores **AND**, **OR** y **NOT** en la calificación de una consulta.
![[Pasted image 20240502102447.png]]

| Operador     | Descripción                                                                           |
| ------------ | ------------------------------------------------------------------------------------- |
| >, <, >=, <= | Mayor que, Menor que, Mayor igual que, Menor igual que                                |
| =, <>        | Igual, Diferente                                                                      |
| BETWEEN      | Entre un rango inclusivo                                                              |
| LIKE         | Búsqueda de un patron. Usa comodines                                                  |
| IN           | Si se conoce el valor exacto que se quiere retornar para al menos una de las columnas |


### Recuperación de datos
```
SELECT A1, ..., An
FROM R1, ..., Rm
WHERE C;
```
- $A_1, \cdots, A_n$ son los nombres de atributos, también se puede utilizar (\*).
- $R_1, \cdots, R_m$ son los nombres de las tablas.
- $C$ es una condición booleana.

**SQL no es sensible a mayúsculas**

### Clausula ORDER BY
Permite ordenar el resultado ascendentemente o descendentemente. Se usa para ordenar el conjunto resultado por una columna específica. De forma predeterminada ordena los registros de forma ascendente.

```
SELECT columnas
FROM tablas
ORDER BY nombre_columna(s) ASC|DESC;
```

### Clausula DISTINCT
Permite filtrar tuplas repetidas

```
SELECT DISTINC columnas
FROM tablas
```


### Clausula LIMIT
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
![[Pasted image 20240502085520.png]]
![[Pasted image 20240502085531.png]]
### Operador IN
Se usa para especificar múltiples valores en una cláusula WHERE.

```
SELECT columnas
FROM tabla
WHERE columna IN (valor1, valor2, ...);
```

![[Pasted image 20240502085335.png]]


### Operador BETWEEN
Usado en una cláusula WHERE para seleccionar un rango de datos entre dos valores.
```
SELECT columnas
FROM tabla
WHERE columna BETWEEN valor1 AND valor2;
```
![[Pasted image 20240502085312.png]]


### Alias
Se puede asignar un alias a una tabla o una columna
```
SELECT columnas
FROM tabla AS alias;

O tambien

SELECT columna AS alias
FrOM tabla;
```
![[Pasted image 20240502085733.png]]



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





# Tipos de datos en PostgreSQL

## VARCHAR
El tipo de datos VARCHAR en SQL se utiliza para almacenar **cadenas de caracteres de longitud variable**. Es útil cuando la longitud de los datos puede variar y no se conoce de antemano su tamaño máximo. Ejemplo
```
CREATE TABLE Ejemplo (
    id INT,
    nombre VARCHAR(50)  -- Define una columna "nombre" que puede contener hasta 50 caracteres.
);
```

- int
- smallint
- double precision
- char(n)
- varchar(n)
- real
- date
- time
- timestamp
- interval
- NUMERIC(precision, scale)


# Eliminar una columna de una tabla

```postgresql
alter table nombre_tabla drop column nombre_campo;
```
