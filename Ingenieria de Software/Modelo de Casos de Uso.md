
- Es usado en los workflows de requerimientos, análisis y diseño y prueba
- **Objetivo**: Comunicar la funcionalidad y el comportamiento al cliente y al usuario (los interesados).

# Casos de uso y actores

## Definiciones

![Actor-Caso-de-uso](https://t2informatik.de/en/wp-content/uploads/sites/2/2019/05/actor-uml-smartpedia.jpg)
### Actor
Representa cualquier cosa que interactúa con el sistema (humano, SW o HW).
Ejemplo: Cajero.

### Caso de Uso
Es una secuencia de acciones que obtienen resultados de un valor para un actor. 
Ejemplo: El proceso de matrícula.
## Actores y ámbito del sistema


![[Pasted image 20240919091909.png]]



## Casos de Uso
- El análisis de los casos de uso incluye entender el dominio de los procesos y el medio externo.
- **¿Cuáles son los actores que participan en los procesos?**
- Los casos e uso describen los procesos y no son realmente artefactos del Análisis Orientado a Objetos.
- Permiten especificar el comportamiento del sistema
	- **El comportamiento es el cómo, el sistema, actúa y reacciona ante el medio
- La especificación de un caso de uso es el documento narrativo que describe la secuencia de eventos que realiza un actor (agente externo) para completar un proceso, a través del uso de un sistema


## Actores
- No son parte del sistema, son roles de un usuario.
- Pueden intercambiar información con el sistema (directo).
- Puede ser un recipiente pasivo de información (indirecto).
- Puede representar a un humano, una máquina o un SW.


# ¿Cómo encontrar los actores?
- Quién está interesado en cierto requerimiento (se beneficia o se ve afectado)
- Dónde en la organización es usado el sistema
- ¿Quiénes usan, eliminan o suministran información?
- ¿Quién usa una determinada función?
- ¿Quién soporta y mantiene el sistema?
- ¿Usa el sistema un recurso externo?
- ¿Cuáles actores necesita el Caso de Uso?
- ¿Un actor juega diferentes roles? o ¿Varios actores juegan el mismo rol (generalización / especialización) ?

# Identificación de los Casos de Uso

## Método basado en los Actores
- Se relacionan los actores vinculados con un **sistema** o **empresa**.
- Para **cada actor**, se identifican los **procesos** que ellos inician o en los que ellos participan

**Preguntas clave**:
- ¿Cuáles son las tareas de este actor?
- ¿Qué objetivos concretos necesita alcanzar un actor?
- ¿Puede el actor crear, almacenar, remover o leer información en el sistema?
- El actor, ¿necesita estar informado acerca de las ocurrencias del sistema?

## Método basado en Eventos
- Se identifican los **eventos externos** a los que un sistema debe responder.
- Se relacionan los **eventos** con los actores y con los **casos de uso**.
- Es útil para este método establecer una tabla de eventos.
- 

## Análisis del modelo de casos de uso del negocio (Business Modeling)

![[Pasted image 20240919093840.png]]
![[Pasted image 20240919093906.png]]


# Escenario de un Caso de Uso
- Un escenario es una instancia de un caso de uso, en donde se dan un conjunto de factores.
- Cada caso de uso tiene un conjunto de escenarios clasificados en:
	- **Primarios o de flujo de eventos normal**: describen cómo trabaja usualmente el sistema
	- **Alternativos**: se producen de acuerdo a excepciones con el escenario primario.

# Casos de Uso y Flujos de Eventos
- La descripción de un caso de uso describe **"que hace"** un sistema, pero no identifica **"cómo"**.
- Un **flujo de eventos** describen el **cómo** (parcialmente) al interior de un caso de uso.
- Cuando se modela, es importante que se conserve la separación de la **vista interna** y **externa**

# Casos de Uso de Alto Nivel
- Describe un proceso muy brevemente, resumiendo la esencia del mismo en breves enunciados.
- Son útiles durante el examen inicial de los requerimientos y del proyecto.
- No influyen de manera determinante en las decisiones de diseño.
- Son similares a los procesos del negocio (automatizables).

| Campo       | Descripción                                                                                                                                |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Caso de Uso | Realizar Préstamo de Libros                                                                                                                |
| Actores     | Socio, Bibliotecario                                                                                                                       |
| Tipo        | Primario                                                                                                                                   |
| Descripción | Un socio elige los libros que desea solicitar en préstamo, luego el bibliotecario los registra como **prestados** y el socio se los lleva. |
| Referencias | *Incluir los requerimientos que están involucrados con el sistema*                                                                         |

# Casos de Uso Esenciales
- Muestra más detalle que uno de alto nivel.
- Tiene una sección destinada al flujo normal de los eventos que los describe paso a paso.
- Tiene muchas secciones destinadas a describir los flujos alternativos


| Campo       | Descripción                                                                                                                                                                                                      |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nombre      | Realizar Préstamo de Libros                                                                                                                                                                                      |
| Actores     | Socio (Iniciador), Bibliotecario                                                                                                                                                                                 |
| Tipo        | Primario y Esencial                                                                                                                                                                                              |
| Propósito   | Capturar un préstamo y sus condiciones de devolución                                                                                                                                                             |
| Descripción | Un socio elige los libros que desea llevarse en préstamo. El bibliotecario registra los libros y consigna su fecha de devolución. El socio se lleva los libros aceptando las condiciones que se le han indicado. |
| Referencias | Requer.:R1, R2 / Anexos: A1, A2                                                                                                                                                                                  |

# Flujo normal de los eventos

| Acción del actor                                                                                | Respuesta del sistema                                   |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| 1. Comienza cuando el socio selecciona libros en calidad de préstamo y se identifica como socio |                                                         |
| 2. El bibliotecario registra el préstamo y los libros solicitados por el socio.                 | 3. Determina fecha de devolución del préstamo           |
| 4. El bibliotecario indica al socio la fecha de devolución del préstamo                         | 5. El sistema retorna el aviso de registro del préstamo |
| 6. El socio se lleva los libros solicitados                                                     |                                                         |
# Pre y Post Condiciones
Describen los cambios de estado del sistema cuando se ejecuta un caso de uso.

>[!tip] Pueden ayudar a identificar las clases...después

## Pre Condiciones
Suposiciones sobre el estado del sistema al iniciarse una operación
- Cosas que son importantes probar en el SW en algún momento de la ejecución
- Cosas que no serán sometidas a pruebas pero de las cuáles depende el éxito de la operación. Ejemplo: Se tiene existencias de productos a distribuir.

## Post Condiciones
- Describen el estado de un sistema luego de ejecutarse un caso de uso.
- No se refieren a las acciones a realizar en un futuro inmediato.
- Se redactan con verbos en pasado.

**Ejemplo**:
- Se creó nueva guía de remisión
- Se actualizó Estado de Orden de Compra (R: Revisado)

### Categorías de Post-Condiciones
- Creación y eliminación de objetos
- Modificación de los atributos
- Asociaciones formadas y canceladas

# Tipos de Casos de Uso

 - **Primario**: Representa los casos más importantes y comunes. Ej.: Alquiler de Libros.
 - **Secundario**: Representan procesos menores o raros. Ej.: Alquiler entre bibliotecas.
 - **Opcional**: Representan que pueden no abordarse. Ej.: Remate de Libros

# Diagramas de Casos de Uso
- Representan un conjunto de casos de uso para un sistema, los actores y **la relación** entre casos de uso y Actores.

## Los sistemas y sus fronteras
Un caso de uso describe la interacción con un **sistema**. Las fronteras ordinarias de un sistema son:
- El hardware/software de un dispositivo o un sistema de cómputo.
- El departamento de una organización (o un empleado de dicho departamento)
- La organización entera.

## Diagrama de Casos de Uso
![[Pasted image 20240919103444.png]]


# Modelo de Casos de Uso
- Tiene un conjunto de instrumentos para comunicarse con el usuario.
- Sólo, no basta. Debe utilizarse en conjunto con el modelo conceptual o diagrama de clases.

## Priorización de Casos de Uso
### En base a la experiencia
- Seleccionar los que incluyan profundamente en la arquitectura básica, dando soporte al dominio y a las capas de servicio de alto nivel o
- Escoger los que presenten el máximo riesgo, funciones urgentes o complejas en las primeras iteraciones.
- Los que requieran investigación a fondo o nueva tecnología.
- Aquellos que representen procesos primarios o la línea de negocio.
- Los que apoyen directamente el aumento de ingresos o la reducción de costos.

### En base a ponderaciones
- Se definen valores a los atributos de los requerimientos.
- Se aplican pesos a los diferentes valores de los atributos.
- Se calcula el peso total de cada requerimiento.
- Se priorizan los requerimientos de mayor peso total

### Notas adicionales
- Debe haber un aso de uso de inicio o arranque.
- Un caso de uso puede abordarse en varias iteraciones incrementándole funcionalidad.

## Organización de los Casos de Uso
Los casos de uso se pueden organizar especificando relaciones de generalización, inclusión o extensión.
### Relación de Generalización
- La generalización entre casos de uso es como la generalización entre clases.
- En concreto, significa que el caso de uso **hijo** adiciona o antepone el **comportamiento** del caso de uso **padre**.

### Relación de Inclusión
- Significa que un caso de uso base **incorpora explícitamente** el comportamiento de otro caso de uso.
- Se usan para evitar describir el mismo flujo de eventos varias veces.
- También se usan para ocultar funcionalidad.
- Es esencialmente un ejemplo de delegación.

### Relación de Extensión
- Significa que existe un caso de uso base que **implícitamente** incorpora el comportamiento de otro caso de uso.
- El caso de uso base puede desarrollarse normalmente, pero ante ciertas **condiciones** sus operaciones pueden **extenderse** al comportamiento de otro caso de uso

### Ejemplo de relaciones
![[Pasted image 20240919104854.png]]


