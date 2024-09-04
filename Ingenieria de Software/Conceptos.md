
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
