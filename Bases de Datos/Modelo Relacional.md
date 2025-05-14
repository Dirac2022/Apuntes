Se basa en la teoría de conjuntos. Esta formado por relaciones, atributos, tuplas y dominios.
Es la base para la mayoría de los SGBD que dominan el mercado.

Una base de datos relacional consiste en una **colección de tablas**.

# Conceptos generales

## Dominio
- Es el conjunto de valores permitidos para un dato.
- Posee una **descripción física** (tipo y formato de los valores que componen el dominio, char(11)) y otra **semántica**  (ayuda en la interpretación de sus valores).
- 
![[Pasted image 20240418101148.png]]

## Atributo
- Es un item de dato de la base de datos
- Posee un nombre y un dominio.

## Tupla
Es un conjunto de pares atributo-valor. El valor de un atributo se define en el momento de la creación de una tupla, este debe ser compatible con el dominio (o *null*). También debe ser **atómico**, es decir, indivisible.

## Relación
Esta compuesto por un encabezado y un cuerpo.
- El encabezado tiene un número fijo de atributos (**grado de la relación**).
- Los atributos no deben ser ambiguos.
- El cuerpo contiene un número variable de tuplas (**cardinalidad de la relación**).
- El orden de las tuplas no es relevante.

## En resumen
- **Relación** es una tabla.
- **Atributo** es un campo o columna de la tabla.
- **Tupla** es una fila de la tabla.
- **Dominio** es el conjunto de valores permitidos de un atributo.


# Base de datos relacional
Una base de datos relacional comprende un conjunto finito no vacío de relaciones. 

## Esquema

El esquema de base de datos se refiere a la estructura lógica y organizativa de una base de datos que describe la forma en que los datos están organizados y relacionados entre sí. En otras palabras, el esquema de base de datos define la arquitectura y el diseño de la base de datos, incluyendo la descripción de las tablas, los campos, las relaciones, las restricciones y otras características importantes.

Hay tres tipos principales de esquemas de base de datos:
1. **Esquema conceptual o lógico**: También conocido como **modelo de datos**, representa la estructura lógica de la base de datos independientemente del hardware o software específico utilizado para implementarla. Este es el nivel más abstracto y se centra en las entidades, los atributos y las relaciones entre ellas. Ejemplos de modelos conceptuales incluyen el Modelo Entidad-Relación (MER) y el Modelo de Datos Relacional.
2. **Esquema físico**: Describe cómo se implementa el esquema conceptual en un sistema de gestión de bases de datos específico. Incluye detalles como la definición de tablas, índices, claves primarias y secundarias, almacenamiento físico de datos en disco, etc. **El esquema físico está más orientado hacia los detalles técnicos de la implementación**.
3. **Esquema externo o de usuario**: Es la visión de la base de datos que tiene un usuario o una aplicación en particular. Puede haber varios esquemas externos que representan diferentes perspectivas de la base de datos para diferentes usuarios. Estos esquemas se definen a través de vistas, que son subconjuntos de datos y operaciones específicas que los usuarios pueden acceder.

El esquema es el conjunto de los esquemas de las relaciones que lo forman. Es decir, si $R_i$ es una relación, y $A_{ij}$ son atributos, el esquema de la base de datos es el conjunto

$R_1 (A_{11}, A_{12},  ... A_{1n})$
$R_2 (A_{21}, A_{22},  ... A_{2n})$
$\vdots$ 
$R_m (A_{m1}, A_{m2},  ... A_{mn})$

## Instancia
Es el conjunto de las instancias de sus relaciones. Una instancia es una "instantánea" de los datos en la base de datos en un determinado instante.
El mismo esquema se puede aplicar a diferentes instancias de una base de datos.

## Esquema e instancia

- **Esquema**
	- Alumno (nombre, matricula, direccion, fechaNac, Curso)
	- Curso (codigo, descripcion)
- **Instancia**
	- (Daniela, 12345, San Diego 310, 28/06/1995, 1)



## Clave
Es un conjunto de uno o más atributos de una relación.
### Clave primaria (Primary Key PK)
Esta formada por un conjunto de atributos cuyos valores **identifican de manera única** una tupla en una relación (Una fila o registro en una tabla). Los valores de los atributos que componen la clave son únicos.

**Alumno**


| Nombre | Matricula    | Direccion         | fechaNac   |
| ------ | ------------ | ----------------- | ---------- |
| Renata | 701034263890 | Las Flores, 210   | 12/11/1990 |
| Vania  | 693529876987 | Guzman Blanco, 35 | 03/07/1996 |
| Maria  | 347685874432 | San Diego 310/34  | 20/02/1995 |

<span style="font-weight:bold">Alumno(</span><span style="font-weight:bold; text-decoration:underline">Matricula</span><span style="font-weight:bold">, Nombre, direccion, fechaNac)</span>

Una clave primaria puede ser compuesta

### Clave candidata
Posee las mismas propiedades que la clave primaria. En el siguiente ejemplo, *Matricula* y *DNI* son claves candidatas.
![[Pasted image 20240418103702.png]]

Las claves candidatas que no son una clave primaria, quedan como **claves alternativas**.

### Clave foránea (Foreign Key FK)
Digamos que tenemos una relación $R_1$ que incluye la clave primaria de otra relación $R_2$. Este atributo se le llama **clave foránea** de $R_1$ referenciando a $R_2$. La clave primaria implementa la "relación" en una base de datos relacional.
![[Pasted image 20240418104323.png]]

<span style="">Alumno(</span><span style="text-decoration:underline">DNI</span><span style="">, Nombre, Direccion, fechaNac, </span><span style="font-weight:bold">nCurso</span><span style="">)</span>
<span style="">Curso (</span><span style="font-weight:bold">Codigo</span><span style="">, Descripcion)</span>
