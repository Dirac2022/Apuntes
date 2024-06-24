
- **Dato**: Es un conjunto de símbolos que no está agregado a ningún conocimiento específico, lo cual lo convierte en inutilizable para quien no sabe el contexto.
- **Información**: Son datos a los que se le han agregado un determinado conocimiento. Una información puede ser interpretada, mientras que un dato solo puede ser visualizado.

## Qué es una base de datos
- Es un conjunto de datos que describe las actividades de una o varias organizaciones relacionadas. 
- Es una colección de datos interrelacionados que representan información sobre un dominio específico.
- Una base de datos es usualmente mantenida y accesada a través de un software conocido como **Sistema Gestor de Base de Datos** (SGDB). Ejemplos: *Oracle*, *Paradox*, *Access*, *PostgreSQL*, *MySQL*, *DBase*, *Interbase*.
- Un **SGBD** es un software que actúa como interfaz entre los datos almacenados en forma binaria en una base de datos y el usuario que desea manejar tales datos.

## Aplicación de las bases de datos
- Banca: clientes, cuentas, préstamos, transacciones bancarias.
- Líneas aéreas: reservas, etc.
- Universidades: estudiantes, matrículas, asignaturas, etc.
- Transacciones de tarjeta de crédito: compras, etc.
- Telecomunicaciones: registros de llamadas, generación mensual de facturas.
- Finanzas: información sobre ventas, compras, documentos financieros.
- Ventas: información de clientes, productos y compras.
- Producción: gestión de la cadena de producción, inventarios, pedidos.
- Recursos humanos: información sobre los empleados, salarios, impuestos, nóminas.

## Objetos de una base de datos
- **Tablas**
- **Vistas**
- **Funciones**
- **Índices**
- **Procedimientos almacenados**
- **Triggers**

## Historia de los Sistemas de Información

| Tecnología              | Año           | Contexto                       | Anotaciones                                                                                                                                                |
| ----------------------- | ------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tarjetas perforadas** | 1980          | Censo en USA                   | Propuesto por **Herman Hollerith**. El equipo de tarjetas perforadas se uso como un medio de entrada para las PC, tanto para los programas como para datos |
| **Cinta magnética**     | 1950          | Primeras computadoras UNIVAC-I | Los datos en estos medios se podían leer en el orden que se almacenaban. **Procesamiento secuencial de archivos**.                                         |
| **Disco magnético**     | Fines de 1950 |                                | Acceso directo a registros. Las actualizaciones se podían hacer al disco sin reescribir todo el archivo.                                                   |

## Evolución de los SGBD

| SGBD / Lenguajes                              | Año           | Creador                            | Contribución                                            |
| --------------------------------------------- | ------------- | ---------------------------------- | ------------------------------------------------------- |
| **Almacén Integrado de Datos - IDS**          | 1960          | Charles Bachman - General Electric | Aporto modelo de datos de red                           |
| **Sistema de Gestión de Información SGBD**    | Fines de 1960 | IBM                                | Modelo jerárquico de datos                              |
| **Modelo de datos relacional**                | 1970          | **Edgar Codd**                     | Hito en el desarrollo de los sistemas de bases de datos |
| **Lenguaje SQL**                              | 1980          | Proyecto System R de IBM           | Lenguaje de consultas estándar                          |
| **SQL**                                       | Fines de 1980 |                                    | Se normaliza este lenguaje (ANSI-ISO)                   |
| **Gestion de transaciones de bases de datos** |               | James Gray                         | El SGBD ejecuta los programas de forma concurrente      |
 

| Ventajas de un SGBD                                         | Desventajas de un SGBD                                                                                                                                                              |
| ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Rapidez en la manipulación y acceso a la información        | Sin dispositivos de control adecuados, la seguridad puede quedar comprometida                                                                                                       |
| Reducción del esfuerzo humano                               | La operación del sistema de base de datos y el desarrollo de aplicaciones necesitan mucha precisión para evitar que informaciones no correspondan a la realidad.                    |
| Disponibilidad de la información                            | La administración del sistema de base de datos puede volverse muy compleja en ambientes distribuidos, con gran volumen de información manipulada por una gran cantidad de usuarios. |
| Control integrado de informaciones distribuidas físicamente |                                                                                                                                                                                     |
| Reducción de redundancia e inconsistencia                   |                                                                                                                                                                                     |
| Compatición de datos entre usuarios o aplicaciones          |                                                                                                                                                                                     |
| Restricciones de seguridad                                  |                                                                                                                                                                                     |
| Reducción de problemas de integridad                        |                                                                                                                                                                                     |



## Lenguajes de base de datos
Un sistema de base de datos provee un **data-definition language** para especificar el esquema de base de datos y un **data-manipulation language** para expresar consultas y actualizaciones de la base de datos. En la práctica ambos lenguajes forman parte de uno solo, por ejemplo, el ampliamente utilizado, lenguaje [[Lenguaje SQL (Structured Query Language)|SQL]]

### Data-Manipulation Language (DML)
Un **lenguaje de manipulación de datos** es un lenguaje que permite a los usuarios acceder o manipular datos organizados según el modelo de datos adecuado. Los tipos de acceso son:

- Obtención de información almacenada en la base de datos
- Inserción de nueva información en la base de datos
- Eliminación de información de la base de datos
- Modificación de información almacenada en la base de datos
 
Básicamente hay dos tipos:
- **Los DML procedimentales** requieren que un usuario especifique qué datos son necesarios y cómo obtener esos datos.
- **Los DML declarativos** (también llamados DML no procedimentales) requieren que un usuario especifique qué datos son necesarios sin especificar cómo obtener esos datos. 
 
Una consulta (**query**) es una declaración que solicita la obtención de información. La parte de un **DML** que implica la obtención de información se llama **lenguaje de consulta**. 

### Data-Definition Language (DDL)
Especificamos un esquema de base de datos mediante un conjunto de definiciones expresado por un lenguaje especial llamado **lenguaje de definición de datos**.

Los sistemas de bases de datos implementan restricciones de integridad que se pueden probar con un mínimo de sobrecarga:

- **Restricciones de Dominio**. Un dominio de valores posibles debe estar asociado con cada atributo (por ejemplo, tipos enteros, tipos de caracteres, tipos de fecha/hora). Declarar un atributo como perteneciente a un dominio particular actúa como una restricción sobre los valores que puede tomar. 

- **Integridad Referencial**. Hay casos en los que deseamos asegurarnos de que un valor que aparece en una relación para un conjunto dado de atributos también aparezca en un cierto conjunto de atributos en otra relación (**integridad referencial**). Por ejemplo, el departamento listado para cada curso debe ser uno que realmente exista. Más precisamente, el valor del nombre del departamento en un registro de curso debe aparecer en el atributo del nombre del departamento de algún registro de la relación de departamento. 

- **Afirmaciones**. Una afirmación es cualquier condición que la base de datos siempre debe cumplir. Las restricciones de dominio y las restricciones de integridad referencial son formas especiales de afirmaciones. Sin embargo, hay muchas restricciones que no podemos expresar utilizando solo estas formas especiales. Por ejemplo, *"Cada departamento debe tener al menos cinco cursos ofrecidos cada semestre*" debe expresarse como una afirmación. Cuando se crea una afirmación, el sistema la prueba para validarla. Si la afirmación es válida, entonces cualquier modificación futura en la base de datos solo se permite si no viola esa afirmación.

- **Autorización**. Es posible que deseemos diferenciar entre los usuarios en cuanto al tipo de acceso que se les permite sobre varios valores de datos en la base de datos. Existen cuatro
	- **Read authorization**
	- **Insert authorization**
	- **Update authorization**
	- **Delete authorization**

El DDL, al igual que cualquier otro lenguaje de programación, recibe como entrada algunas instrucciones (declaraciones) y genera alguna salida. La salida del DDL se coloca en el **diccionario de datos**, que contiene metadatos, es decir, datos sobre datos. El diccionario de datos se considera un tipo especial de tabla que solo puede ser accedida y actualizada por el sistema de bases de datos mismo (no por un usuario regular). **El sistema de bases de datos consulta el diccionario de datos antes de leer o modificar datos reales.**
## SQL (Structured Query Language)
Se subdivide en dos sub-lenguajes
- **DDL** (Data Definition language): Se usa para definir los datos. Es un lenguaje para la definición del esquema de la base de datos y otras propiedades de los datos (CREATE DATABASE, CREATE TABLE, CREATE INDEX).
- **DML** (Data Manipulation Language):  Se usa para generar consultas. (SELECT, INSERT, UPDATE, DELETE).


## Modelo de datos
Es una representación sencilla de estructura de datos reales más complejas. Un modelo de datos ayuda a que el lector entienda las complejidades del ambiente real.

### Modelo Jerárquico
Su estructura lógica básica está representada por una estructura de árbol. La estructura jerárquica contiene **segmentos**. Un segmento es el equivalente de un tipo de registro de un sistema de archivos. Describe un conjunto de relaciones uno a muchos entre un padre y sus segmentos de hijos.

En este modelo, cada entidad tiene solo un padre pero puede tener varios hijos. En la parte superior de la jerarquía, solo hay una entidad que se llama nodo raíz.

![[Pasted image 20240417182453.png]]

#### Características
- La información estaba almacenada en ficheros por orden secuencial.
- Este modelo se establece mediante apuntadores una relación entre los distintos registros de los ficheros.

#### Problemas
- Pesadez en las reorganizaciones de los ficheros.
- Complejidad de implementación
- Falta de independencia estructural
- Anomalías operacionales

### Modelo de Red (1971 - CODASYL)
- Los datos están representados por una **colección de registros** y las relaciones están representadas por **enlaces**.
- Cada registro es una colección de campos, que contiene sólo un valor de datos. Un enlace es una asociación entre dos registros.
- En el modelo de red, **las entidades se organizan en un grafo**, en el que se puede acceder a algunas entidades a través de varias rutas.

![[Pasted image 20240417183339.png]]

En este modelo **cada registro padre puede ser asociado a más de un registro hijo**.

#### Características
- Es simple de implementar.
- Puede manejar muchas relaciones dentro de la organización.
- Tiene **mejor independencia de datos** en comparación con el **modelo jerárquico**.

#### Problemas
- Es más lento que recorrer los ficheros secuencialmente.
- Sistema más complejo de estructura de base de datos.
- Falta de dependencia estructural.

### Modelo Relacional
Se basa en la lógica de predicados y en la teoría de conjuntos (Edgar Codd, 1970).
El lenguaje estándar de las bases de datos relacionales es SQL.

### Modelo Orientado a Objetos
- Multiples tipos de datos se almacenan como **objetos** junto con su código relacionado.
- Puede contener cualquier tipo de dato (videos, música, etc.) junto con los métodos que se utilizarán con esos datos.
- Los objetos se pueden recuperar mediante consultas (Lenguaje de consulta de objetos u OQL).
- Los objetos se pueden reutilizar en otras aplicaciones para crear nuevas aplicaciones rápidamente.

## Modelos de Bases de Datos Híbridas
Es una combinación de dos o más tipos o modelos de bases de datos.
- Híbrido XML/Base de datos relacional.

## Bases de datos Multidimensionales


## Bases de Datos Cloud
En general se alojan en los servidores de un proveedor de base de datos en la [[Cloud Computing Review|nube]] a los que los usuarios pueden acceder a través de la web.
- Los datos a los que uno accede en la red mediante una página web a menudo se almacenan en una base de datos.
- Apoyar y facilitar el comercio electrónico.
- Mostrar información de productos, precios, información del cliente, contenidos del carrito de compras, etc.
- **Las bases de datos en la [[Cloud Computing Review|nube]] permiten que las páginas web sean páginas web dinámicas**.

