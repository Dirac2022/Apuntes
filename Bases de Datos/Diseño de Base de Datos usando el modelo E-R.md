
# Resumen del proceso de diseño

## Fase de diseño
El diseñador de la base de datos debe interactuar con los usuarios de la aplicación para comprender las necesidades de la aplicación, representarlos de una manera de alto nivel que pueda ser entendido por los usuarios, y luego traducir los requisitos en niveles más bajos del diseño.

- La fase inicial del diseño de la base de datos es caracterizar plenamente las necesidades de datos de los usuarios potenciales de la base de datos. El resultado de esta fase es
una especificación de los requisitos del usuario. 

- A continuación, el diseñador elige un modelo de datos y, mediante la aplicación de los conceptos del modelo de datos elegido, traduce estos requisitos en un esquema conceptual de la base de datos. El esquema desarrollado en esta fase de **diseño conceptual** proporciona una visión general de la empresa. El modelo entidad-relación, que estudiamos en el resto de este capítulo, se utiliza típicamente para representar el diseño conceptual. El esquema conceptual especifica las entidades que están representados en la base de datos, los atributos de las entidades, las relaciones entre las entidades, y las limitaciones en las entidades y relaciones. 

- Un esquema conceptual completamente desarrollado también indica los requisitos funcionales de la empresa. En una **especificación de los requisitos funcionales**, los usuarios describen los tipos de operaciones (o transacciones) que se realizarán en los datos. Ejemplo operaciones incluyen la modificación o actualización de datos, la búsqueda y recuperación de datos específicos datos, y la eliminación de datos.

- El proceso de pasar de un modelo de datos abstractos a la implementación de la base de datos procede en dos fases finales de diseño.
	- En la fase de diseño lógico, el diseñador mapea el esquema conceptual de alto nivel en el modelo de datos de aplicación del sistema de base de datos que se utilizará.
	- Finalmente, el diseñador utiliza el esquema de base de datos específico del sistema resultante en la **fase de diseño físico** posterior, en la que se especifican las características físicas de la base de datos. Estas características incluyen la forma de organización de archivos y elección de estructuras de índices.


# Alternativas de diseño
Una parte importante del proceso de diseño de la base de datos es decidir cómo representar en el diseño los diversos tipos de "cosas" tales como personas, lugares, productos, y similares. **Utilizamos el término entidad para referirse a cualquier elemento claramente identificable**. 

Por ejemplo, en una base de datos universitaria, ejemplos de entidades incluirían instructores, estudiantes, departamentos, cursos y cursos. Las diversas entidades están relacionadas entre sí en una variedad de formas, todas las cuales necesitan ser capturado en el diseño de la base de datos. Por ejemplo, un estudiante toma una oferta de curso, mientras
un instructor enseña una oferta de curso; *enseña* y *toma* son ejemplos de relaciones
entre entidades.

Al diseñar un esquema de base de datos, debemos asegurarnos de evitar dos escollos importantes:

## 1. Redundancia
Un mal diseño puede repetir información. El mayor problema con esta representación redundante de la información es que las copias de una información pueden ser inconsistentes si la información se actualiza sin tomar precauciones para actualizar todas las copias de la información.

## 2. Incompletitud
Un mal diseño puede dificultar determinados aspectos de la empresa o imposible de modelar. Evitar los malos diseños no es suficiente. Puede haber un gran número de buenos diseños de la que debemos elegir. Como un simple ejemplo, considere un cliente que compra un producto. ¿Es la venta de este producto una relación entre el cliente y el producto? Alternativamente, es la venta misma una entidad que está relacionada tanto con el cliente como con el producto? Esta elección, aunque simple, puede hacer una diferencia importante en lo que aspectos de la empresa se pueden modelar bien. 

# El modelo Entidad-Relación
El modelo **E-R** fue desarrollado para facilitar el diseño de base de datos permitiendo la especificación de un **esquema empresarial** que represente la estructura lógica general de una base de datos.

El modelo **E-R** emplea tres conceptos básicos: *conjuntos de entidades*, *conjuntos de relaciones* y *atributos*.

## Conjunto de entidades
Una entidad es un *objeto* en el mundo real que es distinguible de todos los otros objetos. Por ejemplo, cada persona en una universidad es una entidad.
Una entidad tiene un conjunto de propiedades, y los valores de algún conjunto de propiedades debe identificar de forma única una entidad.

- Un *conjunto de entidades* es un conjunto de entidades del mismo tipo que comparten las mismas propiedades.
- Los conjuntos de entidades no necesitan ser disjuntos. Por ejemplo, es posible definir una entidad *persona*  que consiste en todas las personas de una universidad. Una entidad *persona* entidad puede ser una entidad *estudiante*, una entidad *instructor* o ambos o ninguno.
- Una entidad está representada por un conjunto de **atributos**. Los atributos son propiedades descriptivas que posee cada miembro de un conjunto de entidades.
- Un conjunto de entidades es representado en un diagrama **E-R** por un **rectángulo**, el cual es dividido en dos partes. La primera, contiene el nombre del conjunto de entidades. La segunda parte contiene los nombres de todos los atributos del conjunto de entidades.

![[Pasted image 20240604112949.png]]


## Conjunto de relaciones
Una **relación** es una asociación entre varias entidades. Un *conjunto de relaciones* es un conjunto de relaciones del mismo tipo.
Considere dos conjuntos de entidad *instructor* y *estudiante*. Definimos el conjunto de relaciones *asesor* para denotar las asociaciones entre los estudiantes y los instructores que actúan como sus asesores. 
![[Pasted image 20240604113317.png]]


Una **instancia de relación** en un esquema E-R representa una asociación entre
entidades nombradas en la empresa del mundo real que está siendo modelada. Como ilustración, la entidad de *instructor* individual Katz, que tiene *ID* de instructor 45565, y la entidad de *estudiante* Shankar, que tiene *ID* de estudiante 12345, participan en una instancia de relación de *asesor*. Esta instancia de relación representa que en la universidad, el instructor Katz esta asesorando al estudiante Shankar.

- Un conjunto de relaciones está representado en un diagrama E-R por un diamante, que está vinculado a través de líneas a un número de diferentes conjuntos de entidades (rectángulos).
![[Pasted image 20240604113618.png]]


### Definición formal
Un conjunto de relaciones es una relación matemática sobre $n \geq 2$ (posiblemente no distintos) conjuntos de entidades. Si $E_1, E_2, \dots, E_n$ son conjunto de entidades, entonces un conjunto de relaciones $R$ es un subconjunto de 
$$
\{ (e_1, e_2, \dots, e_n) | e_1 \in E_1,  \}
$$