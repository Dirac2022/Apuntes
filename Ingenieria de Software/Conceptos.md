edge
# Caso de uso
Un **caso de uso** en el contexto de la ingeniería de software es una herramienta que se utiliza para describir cómo un usuario interactúa con un sistema o aplicación para lograr un objetivo específico. Es una manera estructurada de entender las necesidades del usuario y cómo el sistema debe responder para satisfacer esas necesidades.
### Elementos clave de un caso de uso:

1. **Actor**: Este es el usuario o sistema externo que interactúa con el sistema. En un sistema de software, el actor podría ser una persona (por ejemplo, un cliente o un administrador) o incluso otro sistema que se comunica con el tuyo.

2. **Objetivo**: Cada caso de uso tiene un objetivo claro que el actor quiere lograr. Es el "motivo" de la escena. Por ejemplo, si el actor es un cliente en una tienda en línea, el objetivo podría ser "comprar un producto".

3. **Sistema**: Es el escenario donde se desarrollan las acciones. En la ingeniería de software, esto representa la aplicación o el sistema con el que el actor está interactuando.

4. **Flujo de eventos**: Describe cómo comienza la interacción, qué decisiones se toman, qué hace el sistema en respuesta, y cómo termina la interacción. Un flujo típico podría ser algo así como:
   - El actor inicia sesión en el sistema.
   - El actor busca un producto.
   - El sistema muestra los resultados de la búsqueda.
   - El actor selecciona un producto y lo añade al carrito.
   - El actor finaliza la compra.

5. **Precondiciones**: Son las cosas que deben ser ciertas antes de que comience la escena. Por ejemplo, el actor ya debe estar registrado en el sistema para poder iniciar sesión.

6. **Postcondiciones**: Estas son las condiciones que deberían ser verdaderas después de que el caso de uso se ha completado. Es como asegurarte de que la escena ha terminado de manera satisfactoria. Por ejemplo, después de que el actor completa la compra, el sistema debería haber registrado la transacción y enviar una confirmación al actor.

### Ejemplo de un caso de uso:

Imaginemos un sistema de biblioteca en línea. Un caso de uso podría ser "Buscar un libro". El actor en este caso es un **usuario registrado** que quiere encontrar un libro en el catálogo.

- **Objetivo**: Encontrar un libro específico para ver su disponibilidad.
- **Flujo de eventos**:
  1. El usuario accede al sistema e ingresa sus credenciales.
  2. El usuario selecciona la opción "Buscar libro".
  3. El sistema muestra un cuadro de búsqueda.
  4. El usuario ingresa el título o el autor del libro.
  5. El sistema muestra una lista de libros que coinciden con la búsqueda.
  6. El usuario selecciona un libro para ver más detalles.
- **Precondición**: El usuario debe estar registrado y haber iniciado sesión.
- **Postcondición**: El sistema muestra la disponibilidad del libro seleccionado.

En resumen, un caso de uso es una descripción detallada y estructurada de cómo un usuario interactúa con un sistema para lograr un objetivo. Es como un guion de una película o una obra de teatro, que guía a los desarrolladores para entender cómo debe comportarse el sistema en situaciones específicas.


# Modelo conceptual
Un **modelo conceptual** es una representación abstracta que muestra las principales entidades (o conceptos) que existen en el dominio del problema y las relaciones entre ellas. Es una forma de capturar y representar el conocimiento esencial sobre el dominio para que todos los involucrados (desarrolladores, clientes, usuarios) puedan tener una comprensión común.

#### Analogía: El Mapa de una Ciudad
Imagina que estás diseñando una nueva ciudad. Antes de construirla, creas un mapa que muestra los elementos clave de la ciudad: edificios, calles, parques, ríos, etc., y cómo están conectados entre sí. Este mapa no incluye detalles como los materiales de construcción o el diseño arquitectónico exacto de los edificios, sino que te da una visión general de qué existe en la ciudad y cómo todo se relaciona.

En un **modelo conceptual**:
- **Entidades (o Conceptos)**: Son los "edificios" en tu mapa, los elementos fundamentales del dominio. Por ejemplo, en un sistema de biblioteca, las entidades podrían ser **Libro**, **Usuario**, **Autor**, **Préstamo**.
- **Atributos**: Son las características o propiedades de cada entidad. Siguiendo con la analogía, es como decir que un edificio tiene ciertas características: altura, color, etc. En un modelo conceptual, un **Libro** podría tener atributos como **título**, **ISBN**, **autor**, **año de publicación**.
- **Relaciones**: Son las conexiones entre las entidades, como las calles que conectan diferentes edificios en la ciudad. Por ejemplo, en el sistema de biblioteca, una relación podría ser que un **Usuario** "realiza" un **Préstamo**, y un **Libro** "pertenece" a un **Autor**.

Un modelo conceptual ayuda a identificar y aclarar los elementos esenciales del sistema, sin entrar en los detalles de cómo se implementarán.

# Modelo de Casos de Uso
Un **modelo de casos de uso** es una representación de los diferentes escenarios en los que un usuario interactúa con el sistema para lograr un objetivo. Este modelo se enfoca en las interacciones entre los usuarios (o actores) y el sistema, y se utiliza para identificar y documentar los requisitos funcionales del sistema.


En un **modelo de casos de uso**:
- **Actores**: Son los usuarios o sistemas externos que interactúan con el sistema. Por ejemplo, en un sistema de reservas de vuelos, los actores podrían ser **Pasajero**, **Agente de Viajes**, y **Sistema de Pago**.
- **Casos de Uso**:  Cada caso de uso describe una tarea específica que un actor realiza con el sistema, como "Reservar un vuelo" o "Cancelar una reserva". 
- **Relaciones entre Casos de Uso**: Estas pueden incluir generalización/especialización (donde un caso de uso específico hereda comportamiento de otro más general) o inclusión/extensión (donde un caso de uso incluye la funcionalidad de otro o extiende su comportamiento en ciertas condiciones).

El **modelo de casos de uso** se representa típicamente con diagramas que muestran los actores, los casos de uso y cómo están conectados.

# Pruebas Unitarias y Pruebas de Integración

## Pruebas Unitarias
Las **pruebas unitarias** son pruebas que se centran en verificar el correcto funcionamiento de las unidades más pequeñas de código, como funciones, métodos o clases individuales. Cada unidad se prueba de manera aislada del resto del sistema para asegurar que funciona como se espera.

### Características:
- **Aislamiento:** Se realizan de manera independiente, sin depender de otras partes del sistema.
- **Rápidas:** Debido a que se centran en pequeñas unidades de código, son generalmente rápidas de ejecutar.
- **Automatización:** Frecuentemente se automatizan para ser ejecutadas cada vez que se realizan cambios en el código, permitiendo una retroalimentación rápida.
  
#### Ejemplo:
```python
def suma(a, b):
    return a + b

# Prueba unitaria para la función suma
def test_suma():
    assert suma(2, 3) == 5
    assert suma(-1, 1) == 0
    assert suma(0, 0) == 0
```
En este ejemplo, la prueba unitaria verifica que la función `suma` devuelva los resultados correctos para diferentes casos de prueba.

## Pruebas de Integración
Las **pruebas de integración** se enfocan en verificar que diferentes módulos o componentes del software funcionen correctamente en conjunto. A diferencia de las pruebas unitarias, las pruebas de integración prueban la interacción entre las unidades para asegurarse de que colaboran correctamente.

#### Características:
- **Interacción:** Se centran en la interacción entre módulos o subsistemas, verificando que la integración entre ellos no introduzca errores.
- **Complejidad:** Suelen ser más complejas y lentas que las pruebas unitarias porque involucran varias partes del sistema.
- **Etapas:** Pueden realizarse en diferentes etapas, desde la integración de pequeños grupos de módulos hasta la integración completa del sistema.

#### Ejemplo:
Supongamos que tienes dos módulos: `ModuloUsuario` y `ModuloPedidos`, y quieres probar que juntos funcionan correctamente.
```python
# Módulo que gestiona usuarios
class ModuloUsuario:
    def obtener_usuario(self, user_id):
        # Supongamos que esta función obtiene un usuario de una base de datos
        return {"id": user_id, "nombre": "Juan"}

# Módulo que gestiona pedidos
class ModuloPedidos:
    def crear_pedido(self, usuario, producto):
        # Crea un pedido para un usuario y un producto específico
        return f"Pedido creado para {usuario['nombre']} con el producto {producto}"

# Prueba de integración entre ModuloUsuario y ModuloPedidos
def test_crear_pedido_para_usuario():
    modulo_usuario = ModuloUsuario()
    modulo_pedidos = ModuloPedidos()
    
    usuario = modulo_usuario.obtener_usuario(1)
    resultado = modulo_pedidos.crear_pedido(usuario, "Libro")
    
    assert resultado == "Pedido creado para Juan con el producto Libro"
```

---

### Diferencias Clave

| Aspecto              | Pruebas Unitarias                                           | Pruebas de Integración                                          |
|----------------------|------------------------------------------------------------|-----------------------------------------------------------------|
| **Alcance**          | Unidades individuales (funciones, métodos, clases).         | Interacción entre módulos o componentes.                        |
| **Objetivo**         | Verificar que cada unidad funciona correctamente por sí sola.| Verificar que los módulos funcionan correctamente en conjunto. |
| **Complejidad**      | Baja, ya que se centran en una pequeña parte del código.    | Alta, porque involucra múltiples partes del sistema.            |
| **Velocidad**        | Rápidas de ejecutar.                                        | Más lentas debido a la mayor cantidad de código involucrado.    |
| **Dependencias**     | Sin dependencias de otros módulos o sistemas.              | Requieren que varios módulos funcionen y se comuniquen.         |

Ambos tipos de pruebas son esenciales para un desarrollo de software robusto, ya que permiten detectar errores tanto a nivel de las partes individuales del código como en la interacción entre ellas.



# Stakeholders
https://rockcontent.com/es/blog/que-es-un-stakeholder/
Concepto creado en la década de 1980 por el filósofo estadounidense Robert Edward Freeman, *stakeholder* es cualquier individuo u organización que, de alguna manera, es impactado por las acciones de determinada empresa. En una traducción libre para el español, significa **"partes interesadas"**

Freeman sostenía que los grupos de interés son indispensables y que siempre se deberían tener en cuenta para la planificación estratégica de cualquier negocio.

De esta manera, entender que el triunfo o fracaso de cualquier empresa, siempre afectará no solo a sus dueños sino que también afectará a todos los que la rodean, es decir, **a sus trabajadores, a sus socios, proveedores, competidores, familias de todos los involucrados y por supuesto a sus clientes.**



# Proceso de negocio
Un **proceso de negocio** es un conjunto estructurado de actividades o tareas relacionadas que son realizadas por personas, sistemas o ambos para lograr un objetivo empresarial específico. Estos procesos transforman entradas (inputs) en salidas (outputs) de valor para los clientes o usuarios finales, y pueden involucrar varios departamentos o áreas de una organización. Un buen ejemplo es la gestión de cotizaciones en una agencia de viajes, que incluye la solicitud, creación, aprobación y seguimiento de las cotizaciones.


# Diferencia entre Requerimiento y Caso de Uso

La diferencia entre un **requerimiento** y un **caso de uso** radica en su enfoque y nivel de detalle en el desarrollo del sistema:

### **Requerimiento**
Un **requerimiento** describe lo que el sistema debe hacer o cómo debe funcionar. Puede ser funcional (enfocado en la funcionalidad del sistema) o no funcional (enfocado en las características del sistema).

- **Requerimiento funcional:** Describe una acción o función específica que el sistema debe realizar.
  - Ejemplo: "El sistema debe permitir a los usuarios consultar cotizaciones de paquetes turísticos."
  
- **Requerimiento no funcional:** Establece criterios de calidad o limitaciones sobre cómo debe funcionar el sistema.
  - Ejemplo: "El sistema debe cargar los datos en menos de 3 segundos."

### **Caso de Uso**
Un **caso de uso** es una descripción detallada de cómo los usuarios interactúan con el sistema para cumplir con uno o más requerimientos funcionales. Cada caso de uso describe un flujo completo de interacciones, desde el inicio hasta el resultado final.

- Ejemplo: **Caso de uso - Consulta de cotizaciones por rango de fechas**:
  - Actores: Gerente, agente receptivo.
  - Descripción: El usuario selecciona un rango de fechas y el sistema devuelve las cotizaciones que coinciden.

### Diferencias clave:

| Aspecto               | Requerimiento                               | Caso de Uso                                                   |
|-----------------------|---------------------------------------------|---------------------------------------------------------------|
| **Enfoque**            | Define qué debe hacer el sistema.           | Describe cómo el sistema cumple con el requerimiento.          |
| **Nivel de detalle**   | General o alto nivel.                       | Detallado, incluye actores, pasos, variaciones y excepciones.  |
| **Objetivo**           | Especificar funcionalidad o restricciones.  | Describir escenarios de interacción entre usuario y sistema.   |
| **Formato**            | Declaración específica o lista de requisitos. | Narrativa que explica los pasos de la interacción.             |

En resumen, los **requerimientos** describen las funcionalidades y limitaciones del sistema, mientras que los **casos de uso** detallan cómo se lleva a cabo cada interacción entre los usuarios y el sistema para cumplir con esos requerimientos.



# Relaciones entre Casos de Uso
En un **diagrama de casos de uso**, las relaciones entre casos de uso se utilizan para mostrar cómo los distintos casos están conectados o dependen entre sí. Los tres tipos principales de relaciones son **generalización**, **inclusión** y **extensión**. A continuación te explico cada una con ejemplos y cómo se representan en los diagramas.

### 1. **Generalización**
La **generalización** se usa cuando un caso de uso más específico hereda las propiedades de un caso de uso más general. La generalización implica que un caso de uso hijo puede reemplazar al caso de uso padre, ya que contiene toda la funcionalidad del padre, más algunas particularidades adicionales.

- **Ejemplo**: 
  - Caso de uso padre: "Realizar Pago".
  - Caso de uso hijo: "Realizar Pago con Tarjeta" y "Realizar Pago con PayPal".
  
  En este caso, "Realizar Pago" es un caso de uso general, y los casos de uso "Realizar Pago con Tarjeta" y "Realizar Pago con PayPal" son casos más específicos que heredan la funcionalidad básica de realizar un pago, pero añaden detalles específicos de cada método.

- **Representación en el diagrama**:
  - Se utiliza una flecha con la punta vacía apuntando desde el caso de uso específico (hijo) al caso de uso general (padre). 

  ![Generalización](https://upload.wikimedia.org/wikipedia/commons/5/58/Use_case_generalization.png)

### 2. **Inclusión (Include)**
La **inclusión** se usa cuando un caso de uso siempre **depende de otro** para completarse, es decir, un caso de uso incluye el comportamiento de otro. El caso de uso incluido se invoca siempre como parte del flujo del caso de uso principal.

- **Ejemplo**:
  - Caso de uso principal: "Reservar un Paquete Turístico".
  - Caso de uso incluido: "Iniciar Sesión".

  En este ejemplo, antes de que un usuario pueda reservar un paquete turístico, siempre debe iniciar sesión. El caso de uso "Iniciar Sesión" es requerido por "Reservar un Paquete Turístico".

- **Representación en el diagrama**:
  - Se usa una flecha discontinua con la etiqueta `<<include>>` apuntando desde el caso de uso principal hacia el caso de uso incluido.

  ![Inclusión](https://upload.wikimedia.org/wikipedia/commons/3/3f/Use_case_include.png)
  

### 3. **Extensión (Extend)**
La **extensión** se utiliza cuando un caso de uso adicional **se activa condicionalmente** en un flujo particular del caso de uso principal. A diferencia de la inclusión, donde el caso de uso secundario siempre se ejecuta, la extensión es opcional y depende de ciertas condiciones.

- **Ejemplo**:
  - Caso de uso principal: "Procesar Cotización".
  - Caso de uso extendido: "Agregar Observaciones a la Cotización".

  En este caso, "Agregar Observaciones a la Cotización" solo se activará si el socio decide hacerlo, es decir, es una acción opcional dentro del caso de uso "Procesar Cotización".

- **Representación en el diagrama**:
  - Se usa una flecha discontinua con la etiqueta `<<extend>>` apuntando desde el caso de uso extendido hacia el caso de uso principal.

  ![Extensión](https://upload.wikimedia.org/wikipedia/commons/5/58/Use_case_extend.png)

### Diferencias clave:

| Relación        | Descripción                                                | Cuándo usarla                                                                 | Representación                                                                                                 |
|-----------------|------------------------------------------------------------|-------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| **Generalización** | Un caso de uso hijo hereda la funcionalidad del caso padre. | Cuando existen variaciones de un mismo proceso que comparten características. | Flecha sólida con la punta vacía apuntando del hijo al padre.                                                  |
| **Inclusión**      | Un caso de uso depende siempre de otro para completarse.  | Cuando un caso de uso requiere siempre la ejecución de otro.                  | Flecha discontinua con la etiqueta `<<include>>` apuntando del caso de uso principal al caso de uso incluido.  |
| **Extensión**      | Un caso de uso se activa de manera condicional.          | Cuando una funcionalidad es opcional o se activa solo bajo ciertas condiciones. | Flecha discontinua con la etiqueta `<<extend>>` apuntando del caso de uso extendido al caso de uso principal. |

Estas relaciones son clave para estructurar correctamente los diagramas de casos de uso, mostrando cómo interactúan los diferentes procesos en un sistema.

# Características
Las **características** (también conocidas como *features* en inglés) son aspectos clave del sistema o producto que describen lo que este puede hacer. Son propiedades o funcionalidades de alto nivel que definen las capacidades del sistema. Estas características están orientadas al usuario final y responden a las preguntas: **¿qué ofrece el sistema?** o **¿qué puede hacer el usuario con el sistema?**

Por ejemplo, para la agencia de viajes Perú TOURS, algunas características podrían ser:
- Afiliar nuevos clientes no socios.
- Permitir a los socios solicitar paquetes turísticos.
- Permitir a los socios consultar y aprobar cotizaciones.
- Registrar el pago de las cotizaciones aprobadas.
- Consultar cotizaciones por rango de fechas.

### Relación entre **Características** y **Casos de Uso**
Las características están estrechamente relacionadas con los **casos de uso**, ya que los casos de uso detallan cómo se ejecutan las características en el sistema. Dicho de otra manera, **los casos de uso describen la interacción entre los actores y el sistema para implementar las características del sistema**.

- **Características**: Definen lo que el sistema puede hacer.
- **Casos de uso**: Detallan cómo el sistema y los actores interactúan para lograr esas características.

### Ejemplo de Relación:
Supongamos que una de las características del sistema de la agencia de viajes es **Afiliar Socios**. Para implementar esta característica, se desarrolla un caso de uso específico que describe los pasos que un cliente no socio sigue para completar su afiliación en el sistema:

| **Característica**                  | **Caso de Uso**                             |
|-------------------------------------|---------------------------------------------|
| **Afiliar nuevos clientes no socios**| Caso de Uso: Afiliar Socio                  |
| **Solicitar paquetes turísticos**    | Caso de Uso: Comprar Paquete Turístico      |
| **Consultar cotizaciones por fechas**| Caso de Uso: Consultar Cotizaciones por Fecha|

### Diferencias y Relación:
| **Característica**                            | **Caso de Uso**                                  |
|-----------------------------------------------|--------------------------------------------------|
| Descripción de una funcionalidad a nivel alto. | Descripción detallada de cómo los usuarios interactúan con el sistema para lograr una funcionalidad. |
| Generalmente orientada al **qué** hace el sistema. | Enfocado en el **cómo** se lleva a cabo la interacción para realizar la característica. |
| Pueden ser pocas y abarcan amplias funciones.  | Pueden existir múltiples casos de uso para cada característica, que detallan diferentes flujos de interacción. |

### Conclusión:
Las **características** definen las funcionalidades generales que ofrece un sistema, mientras que los **casos de uso** describen en detalle cómo esas características se realizan a través de interacciones concretas entre los actores y el sistema. Por lo tanto, cada característica generalmente está asociada con uno o más casos de uso.



# Agregación y composición

En el modelado de negocio y en la ingeniería de software, **agregación** y **composición** son dos tipos de relaciones entre objetos o clases que se utilizan comúnmente en el diagrama de clases de UML (Unified Modeling Language). Estas relaciones ayudan a entender cómo los objetos interactúan y dependen entre sí dentro de un sistema.

### Definiciones

| Término         | Definición                                                                                                                                                                                                                                    | Características Clave                                                                                                        |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Agregación**  | Es una relación "débil" de todo a parte donde los objetos pueden existir independientemente entre sí. Representa que una clase contiene o agrupa objetos de otra clase, pero los objetos no dependen del ciclo de vida del objeto contenedor. | - Representado por una línea con un rombo vacío en UML.<br>- Los objetos pueden existir sin su contenedor.                   |
| **Composición** | Es una relación "fuerte" de todo a parte donde los objetos son dependientes entre sí. La vida del objeto dependiente (parte) está atada a la vida del objeto contenedor (todo). Si el todo es destruido, las partes también lo son.           | - Representado por una línea con un rombo relleno en UML.<br>- Los objetos parte no pueden existir sin el objeto contenedor. |

---

### Uso en UML

En un **diagrama de clases UML**, las relaciones de agregación y composición se representan gráficamente para mostrar cómo los objetos se relacionan entre sí. Estas relaciones son fundamentales para definir la estructura interna de un sistema y comprender cómo interactúan los objetos.

- **Agregación**: Indica que una clase "tiene" una o más instancias de otra clase, pero estas instancias pueden existir independientemente.
- **Composición**: Define una relación en la que las instancias de la clase "parte" no pueden existir sin la instancia de la clase "todo".

---

### Ejemplo Práctico

Imaginemos que estamos modelando un sistema de gestión para una **biblioteca**. Vamos a ver cómo aplicamos **agregación** y **composición** en este contexto.

| Ejemplo                   | Tipo de Relación | Descripción                                                                                                                                                                                                                      |
|---------------------------|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Biblioteca y Libros**    | Agregación       | Una **Biblioteca** puede tener varios **Libros**. Si se cierra la biblioteca, los libros siguen existiendo. Los libros pueden ser prestados o trasladados a otra biblioteca. Aquí la biblioteca agrupa los libros, pero no es "dueña" de ellos. |
| **Libro y Capítulos**      | Composición      | Un **Libro** está compuesto por varios **Capítulos**. Si el libro se destruye, los capítulos también lo hacen, ya que no tienen sentido fuera del libro. Los capítulos son parte integral del libro y no pueden existir por sí solos.        |

### Ejemplo UML

1. **Agregación**:
    - Relación entre `Biblioteca` y `Libro`: 
      - En UML, se dibuja una línea que conecta `Biblioteca` con `Libro`, con un rombo vacío en el extremo que conecta a la `Biblioteca` para indicar la agregación.
      
2. **Composición**:
    - Relación entre `Libro` y `Capítulo`:
      - Se dibuja una línea entre `Libro` y `Capítulo`, con un rombo relleno en el extremo de `Libro`, indicando que un libro compone sus capítulos.

---

| Clase       | Atributos          | Métodos                  |
|-------------|--------------------|--------------------------|
| **Biblioteca** | nombre, dirección   | añadirLibro(), eliminarLibro() |
| **Libro**      | título, autor       | abrir(), cerrar()          |
| **Capítulo**   | número, título      | leer(), marcar()           |

Con estas relaciones de agregación y composición, estamos representando claramente cómo los objetos interactúan en el sistema de gestión de biblioteca.


# Clases de análisis
En la ingeniería de software, especialmente en el diseño orientado a objetos, las clases se pueden categorizar en clases de interfaz, de control y de entidad. Cada tipo de clase juega un papel específico en la estructura y funcionamiento de un sistema. Vamos a explorar cada uno de estos tipos de clases y cómo interactúan en el contexto de un caso de uso.

### 1. Clases de Entidad
Las **clases de entidad** representan objetos que contienen información importante para el sistema. Su principal responsabilidad es almacenar datos y persistir a lo largo del tiempo. Estos objetos suelen corresponder a las tablas en una base de datos.

### 2. Clases de Interfaz
Las **clases de interfaz** son aquellas que interactúan directamente con los usuarios o con otros sistemas. Facilitan la entrada y salida de datos, presentando la información al usuario y/o solicitando datos del mismo.

### 3. Clases de Control
Las **clases de control** sirven como mediadoras entre las clases de interfaz y las clases de entidad. Manejan la lógica y el flujo de operaciones en los casos de uso, coordinando cómo se utilizan las clases de entidad y cómo se presentan los resultados a través de las clases de interfaz.

### Ejemplo Real: Sistema de Reservación de Hotel
Imaginemos que estamos diseñando un sistema para gestionar reservaciones en un hotel. El caso de uso principal es "Realizar una Reservación".

#### Detalle de Clases

| Tipo de Clase | Nombre de Clase | Responsabilidades |
|---------------|-----------------|-------------------|
| Entidad       | Reservación     | Almacenar los detalles de las reservaciones, como fechas, tipo de habitación, cliente. |
| Entidad       | Cliente         | Mantener información del cliente como nombre, contacto, preferencias. |
| Interfaz      | UIReservaciones | Mostrar formularios para ingresar datos de la reservación, mostrar confirmaciones y errores. |
| Control       | ControladorReservaciones | Procesar las entradas del usuario, validarlas, interactuar con objetos de Reservación y Cliente para almacenar datos y luego enviar la respuesta al usuario a través de UIReservaciones. |

#### Flujo de Interacción en el Caso de Uso "Realizar una Reservación"

1. **Inicio**: El usuario inicia la interfaz UIReservaciones.
2. **Entrada de Datos**: El usuario introduce los detalles de su reservación.
3. **Procesamiento de Datos**: ControladorReservaciones toma la entrada del usuario.
   - Valida los datos.
   - Crea/modifica objetos de la clase Reservación y Cliente según sea necesario.
   - Persiste los cambios en la base de datos.
4. **Respuesta al Usuario**: UIReservaciones muestra una confirmación o mensajes de error basados en la respuesta del controlador.

Este ejemplo demuestra cómo las clases de control, interfaz y entidad trabajan conjuntamente para realizar operaciones cruciales en un sistema, en este caso, para llevar a cabo una reservación en un hotel.




# Mecanismos de Abstracción en el Modelado de Clases

1. **Clasificación / Instanciación**:
   - **Clasificación** es el proceso de agrupar objetos o conceptos en clases basándose en características comunes. En los diagramas de clases, una **clase** representa una categoría general de objetos con atributos y métodos similares.
   - **Instanciación** se refiere a la creación de instancias o **objetos** de una clase. Un objeto es una entidad particular de una clase que tiene valores específicos de los atributos definidos en la clase.

   | Concepto       | Descripción                                                                 |
   |----------------|-----------------------------------------------------------------------------|
   | **Clasificación** | Agrupar objetos o entidades que comparten características comunes.         |
   | **Instanciación**| Crear un objeto individual que es una instancia de una clase definida.     |

2. **Composición / Descomposición**:
   - **Composición** es una relación entre clases donde una clase "contenedora" está formada por otras clases más simples (componentes). Si el contenedor se destruye, sus componentes también se destruyen. Es un tipo de relación "todo-parte".
   - **Descomposición** es el proceso inverso, donde se desglosa un sistema complejo en partes más simples o componentes, lo que facilita su análisis o diseño.

   | Concepto         | Descripción                                                                               |
   |------------------|-------------------------------------------------------------------------------------------|
   | **Composición**   | Relación fuerte entre un objeto contenedor y sus componentes (dependencia total).         |
   | **Descomposición**| Dividir un sistema o problema en partes más pequeñas para su manejo o análisis.           |

3. **Agrupación / Individualización**:
   - **Agrupación** es un mecanismo para combinar varios objetos o clases en un conjunto, lo que permite tratarlos como una única entidad en ciertos contextos.
   - **Individualización** es el proceso de identificar y tratar objetos como entidades únicas y separadas dentro de un grupo.

   | Concepto             | Descripción                                                                            |
   |----------------------|----------------------------------------------------------------------------------------|
   | **Agrupación**        | Reunir varios objetos o clases en una colección para manejarlos como una sola entidad. |
   | **Individualización** | Tratar a los objetos o clases como entidades únicas y separadas.                       |

4. **Especialización / Generalización**:
   - **Generalización** es el proceso de definir una clase más genérica a partir de varias clases más específicas que comparten características comunes. Esto permite reducir la redundancia mediante la creación de una **superclase** que engloba los atributos y comportamientos comunes.
   - **Especialización** es el proceso inverso, en el cual se crean subclases a partir de una clase genérica, agregando características más específicas.



   | Concepto              | Descripción                                                                                   |
   |-----------------------|-----------------------------------------------------------------------------------------------|
   | **Generalización**     | Crear una clase general a partir de otras más específicas, capturando características comunes.|
   | **Especialización**    | Definir subclases a partir de una clase base, añadiendo atributos y métodos más específicos.   |


Estos mecanismos de abstracción permiten que el diseño de sistemas complejos se maneje de manera eficiente y organizada, facilitando el análisis, la implementación y el mantenimiento del software. En los diagramas de clases de UML, se usan para representar relaciones entre objetos y clases, y cómo estas interacciones dan forma a la estructura del sistema.



# Inyección de dependencias

### 1. **¿Qué es una inyección de dependencias? ¿Qué es una dependencia?**

**Dependencia**: En programación, una dependencia es un objeto o componente que una clase o módulo necesita para funcionar. Por ejemplo, si una clase `A` necesita interactuar con una clase `B` para realizar su tarea, `B` se considera una dependencia de `A`. Tradicionalmente, en la programación orientada a objetos, la clase `A` crea la instancia de la clase `B` dentro de su código.

**Inyección de Dependencias**: La **inyección de dependencias (DI)** es un patrón de diseño que permite reducir el acoplamiento entre clases al delegar la responsabilidad de crear las dependencias de una clase a un componente externo. En lugar de que una clase cree directamente sus dependencias, el contenedor de DI (en el caso de Spring, el _ApplicationContext_) se encarga de instanciarlas y "inyectarlas" en la clase cuando es necesario.

### **¿Cómo funciona la inyección de dependencias en Spring?**

Spring gestiona la creación y administración de objetos (instancias de clases) y las relaciones entre ellos a través de su contenedor de **Beans**. Cuando se inyectan dependencias, Spring se encarga de crear las instancias de las clases dependientes y las proporciona a las clases que las requieren (sin que ellas tengan que saber cómo crearlas). Esto reduce el acoplamiento entre clases y facilita las pruebas unitarias y el mantenimiento del código.

Por ejemplo:

- **Sin inyección de dependencias**: La clase `HotelService` tendría que crear una instancia de `HotelRepository` de manera explícita en su código.
- **Con inyección de dependencias**: Spring se encarga de crear y pasar la instancia de `HotelRepository` cuando crea la instancia de `HotelService`.

java

Copiar código

`@Autowired HotelRepository hotelRepository;`

El código anterior indica que Spring debe inyectar automáticamente la instancia de `HotelRepository` en la clase `HotelService` en el momento en que se cree.


# Consultas personalizadas en JPA

### **¿Qué es una consulta personalizada en Spring Data JPA?**

Cuando hablamos de consultas personalizadas en **Spring Data JPA**, nos referimos a la capacidad que tiene Spring de generar automáticamente las consultas SQL (o JPQL, que es la variante de JPA) basadas en el nombre de los métodos que defines en los repositorios. Este comportamiento está basado en **convenciones de nomenclatura** que Spring Data JPA interpreta y transforma en una consulta de base de datos.

Por ejemplo, el método `findByCiudad` sigue una convención que Spring Data JPA puede entender para crear una consulta que busque los hoteles de una ciudad en particular. No necesitas escribir explícitamente la consulta SQL o JPQL, sino que Spring la genera automáticamente. Este comportamiento es una característica que hace que **Spring Data JPA** sea muy potente y que puedas acceder a la base de datos de manera declarativa y sin tener que escribir código SQL explícito.

### **¿Cómo funciona la convención de Spring Data JPA?**

Spring Data JPA sigue una convención de nomenclatura de los métodos que se interpreta de la siguiente manera:

- **`findBy`**: Indica que este es un método de búsqueda.
- **`Ciudad`**: Es el nombre del atributo que deseas usar para filtrar los resultados. En este caso, `Ciudad` es el nombre de la propiedad de la entidad `Hotel` que hace referencia a la ciudad en la que se encuentra el hotel. Spring Data JPA entiende que esta propiedad corresponde a una relación con la entidad `Ciudad`.

#### Ejemplo:

```java
List<Hotel> findByCiudad(Ciudad ciudad);
```

Este método sigue la convención y se traduce automáticamente por Spring Data JPA en una consulta SQL o JPQL equivalente a algo como:

- **SQL**:
    
    ```sql
    SELECT * FROM hotel WHERE ciudad_id = ?;
    ```
    
    Aquí, `ciudad_id` es la columna en la tabla `hotel` que hace referencia a la entidad `Ciudad` (como definimos en la entidad `Hotel` con la anotación `@JoinColumn`).
    
- **JPQL** (si se usara en lugar de SQL):
    
    ```jpql
    SELECT h FROM Hotel h WHERE h.ciudad = :ciudad;
    ```
    
    Este es el equivalente de la consulta en JPQL, que es un lenguaje de consultas orientado a objetos utilizado por JPA. El `:ciudad` es un parámetro que se usa para filtrar los resultados por la ciudad proporcionada.
    

### **¿Qué pasa si no sigues la convención?**

Si no sigues la convención en el nombre del método, **Spring Data JPA no podrá generar la consulta automáticamente**. Spring necesita que el nombre del método esté bien estructurado según la convención de nomenclatura para entender qué tipo de consulta deseas realizar. Si no sigues la convención, tendrás que escribir una consulta personalizada explícitamente utilizando la anotación `@Query` o utilizando `Criteria API`.

Por ejemplo, si en lugar de `findByCiudad` pusieras `obtenerHotelesPorCiudad`, Spring no podría generar la consulta automáticamente y **fallaría** a menos que se le indicara cómo hacerlo explícitamente.


- **Spring Data JPA** interpreta el nombre de métodos como `findByCampo` y los traduce automáticamente en consultas SQL o JPQL. Esta traducción ocurre **sin necesidad de escribir el código SQL explícitamente**.
- Si no sigues la convención de nomenclatura, **Spring no podrá generar la consulta automáticamente** y necesitarás escribir la consulta manualmente con `@Query`.

---

### **Ejemplo de un método con convención de Spring Data JPA:**

Veamos un ejemplo detallado del funcionamiento de la convención con `findByCiudad`:

#### La entidad `Hotel`:

```java
@Entity
public class Hotel {
    @ManyToOne
    @JoinColumn(name="ciudad_id")
    private Ciudad ciudad;
}
```

#### La interfaz `HotelRepository`:

```java
@Repository
public interface HotelRepository extends JpaRepository<Hotel, Long> {
    // Spring generará una consulta para buscar todos los hoteles de una ciudad.
    List<Hotel> findByCiudad(Ciudad ciudad);
}
```

En este ejemplo, el método `findByCiudad` hace lo siguiente:

1. **`findBy`**: Indica que estamos buscando (`find`) algo.
2. **`Ciudad`**: Hace referencia al atributo de la entidad `Hotel` que representa la ciudad.
    - Spring toma el nombre del atributo `ciudad` y lo usa para construir la consulta.

El resultado es una consulta que seleccionará todos los hoteles de la base de datos que tengan una ciudad específica.

#### ¿Qué hace Spring con este método?

Cuando llamamos al método `findByCiudad`, Spring Data JPA:

1. **Crea una consulta SQL**: Internamente, Spring crea una consulta SQL que selecciona todos los hoteles que corresponden a la ciudad proporcionada.
    
    - En SQL, la consulta generada podría ser algo como:
        
        ```sql
        SELECT * FROM hotel WHERE ciudad_id = ?;
        ```
        
    - Aquí, `ciudad_id` es la columna que hace referencia a la ciudad, y el `?` es el parámetro que se reemplazará con el valor de la ciudad que le pases al método.
        
2. **Ejecuta la consulta en la base de datos**: Spring ejecuta la consulta generada y mapea los resultados de la base de datos de vuelta a objetos `Hotel`.
    

---

### **¿Y si no quiero seguir la convención?**

Si deseas escribir una consulta que no sigue la convención o necesitas más flexibilidad, puedes usar la anotación `@Query` de Spring Data JPA para escribir la consulta de forma explícita. Aquí tienes un ejemplo:

#### Usando `@Query` para consultas personalizadas:

```java
@Repository
public interface HotelRepository extends JpaRepository<Hotel, Long> {

    @Query("SELECT h FROM Hotel h WHERE h.ciudad = :ciudad")
    List<Hotel> buscarHotelesPorCiudad(@Param("ciudad") Ciudad ciudad);
}
```

- **`@Query`**: Define una consulta personalizada usando JPQL.
- **`:ciudad`**: Es un parámetro que se reemplazará con el valor que se pase al método.
- **`@Param("ciudad")`**: Especifica el nombre del parámetro en la consulta y lo vincula al parámetro del método.

Este método hace lo mismo que `findByCiudad`, pero usando una consulta personalizada.


# REST
### ¿Qué es REST?

**REST** (Representational State Transfer) es un estilo de arquitectura de software que se utiliza principalmente para diseñar servicios web. REST se basa en una serie de principios y restricciones que permiten la creación de aplicaciones distribuidas de manera escalable y sencilla. Un servicio RESTful utiliza los métodos estándar de HTTP (GET, POST, PUT, DELETE) para realizar operaciones sobre los recursos (entidades), que se representan generalmente en formato JSON o XML.

En REST:

- **Los recursos** son las entidades (como `Hotel`, `Ciudad`, etc.), identificadas por una URL.
- **Las operaciones** sobre los recursos corresponden a las acciones estándar HTTP:
    - **GET**: Obtener información de un recurso.
    - **POST**: Crear un nuevo recurso.
    - **PUT**: Actualizar un recurso.
    - **DELETE**: Eliminar un recurso.

**Ventajas de REST:**

- **Escalabilidad**: Permite que el sistema se distribuya fácilmente.
- **Simplicidad**: Utiliza los métodos HTTP estándar y no requiere complejos esquemas de comunicación.
- **Estándares universales**: Basado en principios bien establecidos, por lo que es fácil de entender y usar en diferentes plataformas.




