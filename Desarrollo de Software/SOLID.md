
# Principios SOLID en Python

Los principios **SOLID** son un conjunto de buenas prácticas de diseño orientado a objetos que ayudan a crear software más mantenible, comprensible y flexible. Fueron definidos por Robert C. Martin (conocido como “Uncle Bob”) y popularizados por Michael Feathers (quien acuñó el acrónimo SOLID). En pocas palabras, como señalan Martin y Feathers, estos principios _“nos alientan a crear software más fácil de mantener, comprensible y flexible”_. Esto significa que a medida que nuestras aplicaciones crecen, SOLID ayuda a reducir la complejidad y los _“dolores de cabeza”_ futuros. Además, en un entorno de desarrollo con enfoque DevOps (CI/CD, pruebas automatizadas con pytest, control de versiones en GitHub, etc.), aplicar SOLID facilita la integración continua y las pruebas unitarias, ya que genera código modular y desacoplado que se puede testear y desplegar de forma independiente.

## 🔍 Principio de Responsabilidad Única (SRP)

**Teoría:** El principio de responsabilidad única (Single Responsibility Principle, SRP) establece que una clase **debe tener una única razón para cambiar**. En otras palabras, cada clase debe enfocarse en una sola responsabilidad o propósito específico. Si una clase está haciendo más de una tarea, estará demasiado acoplada y será frágil: un cambio en una funcionalidad puede afectar las demás. Como explica Software Crafters, _“ninguna clase debería tener más de un único motivo para cambiar”_. Esto mejora la mantenibilidad, pues las funcionalidades quedan aisladas. Por ejemplo, si mezclamos lógica de acceso a base de datos con lógica de negocio en la misma clase, cualquier cambio en el motor de base de datos obligaría a modificar esa clase, incluso si la lógica de negocio no cambió. Aplicar SRP evita que arreglar un error en una parte del código introduzca un bug en otra parte no relacionada. Por ello, cada clase debería representar una entidad concreta (p. ej. un modelo de dominio como “Usuario”, “Producto” o “Factura”) **o** un servicio auxiliar específico (como “Repositorio de usuarios” o “Generador de reportes”), pero no ambos.

**Ejemplo en Python:** Supongamos un sistema de e-commerce donde tenemos una clase que maneja tanto la lógica de la orden como su impresión. Este diseño viola SRP porque la clase `Order` tiene dos responsabilidades: calcular el total y mostrar la orden. Luego mostramos la versión corregida separando responsabilidades:

```python
# Ejemplo SIN SRP: una clase Order con múltiples responsabilidades
class Order:
    def __init__(self, items, prices):
        self.items = items            # Lista de items en la orden
        self.prices = prices          # Lista de precios correspondientes
    def total(self):
        # Calcula el total sumando todos los precios
        return sum(self.prices)
    def print_order(self):
        # Imprime el detalle de la orden y su total
        print("Orden:")
        for item, price in zip(self.items, self.prices):
            print(f"- {item}: ${price}")
        print(f"Total: ${self.total()}")
```

En el código anterior, la clase `Order` **tiene dos responsabilidades**: por un lado calcula el total, por otro imprime la orden. Si queremos cambiar la forma de imprimir o enviar la orden (por ejemplo, a un archivo, por email o en formato JSON), tendríamos que modificar `Order`, lo cual viola SRP. Además, mezclar la lógica de negocio (calcular total) con la presentación dificulta las pruebas unitarias y la reutilización.

La solución es extraer la responsabilidad de impresión a otra clase dedicada:

```python
# Ejemplo con SRP: separamos la lógica de orden y de impresión
class Order:
    def __init__(self, items, prices):
        self.items = items            # Lista de items en la orden
        self.prices = prices          # Lista de precios correspondientes
    def total(self):
        # Calcula el total sumando todos los precios
        return sum(self.prices)

class OrderPrinter:
    def print(self, order: Order):
        # Imprime el detalle de la orden y su total, usando un objeto Order
        print("Orden:")
        for item, price in zip(order.items, order.prices):
            print(f"- {item}: ${price}")
        print(f"Total: ${order.total()}")
```

En este diseño **cada clase tiene una sola responsabilidad**. La clase `Order` sólo se encarga de almacenar los datos de la orden y calcular su total; no sabe nada de cómo mostrarlos. Por su parte, `OrderPrinter` sólo se encarga de la presentación de una orden. Ahora, si se requiere cambiar el formato de salida (por ejemplo, generar un PDF o un JSON), sólo modificaríamos o extenderíamos `OrderPrinter` o crearíamos otra clase especializada, sin tocar la clase `Order`. Este acoplamiento débil facilita el mantenimiento: podemos probar y desplegar cada parte por separado y evita que un cambio en la impresión rompa la lógica de cálculo de la orden.

**Caso práctico:** En un sistema bancario, podríamos tener una clase `CuentaBancaria` que maneja cálculos de intereses y operaciones de balance, y otra clase `NotificadorMovimientos` que envía alertas. Si mezcláramos ambas, cualquier cambio en el sistema de notificaciones (p. ej. enviar SMS en lugar de email) forzaría a cambiar la clase de la cuenta, algo innecesario. En cambio, aplicando SRP cada clase sólo cambia si cambia su propia función, reduciendo errores imprevistos.

## 🧩Principio Abierto/Cerrado (OCP)

**Teoría:** El principio abierto/cerrado (Open/Closed Principle, OCP) dice que los ==**elementos de software deben estar abiertos para su extensión, pero cerrados para su modificación**==. Es decir, el comportamiento de una clase o módulo debe poder ampliarse (por ejemplo, agregando nuevas funcionalidades) sin tener que modificar su código fuente original. De este modo, el código existente permanece estable (cerrado) y los cambios se logran mediante la herencia, composición o inyección, creando nuevos módulos adicionales (abiertos).

En la práctica, esto significa que si necesitamos añadir soporte para un nuevo caso (p. ej. una nueva forma geométrica, un nuevo tipo de descuento o un nuevo método de pago), preferimos **extender** el sistema con clases o módulos nuevos que cumplan con la interfaz esperada, en lugar de editar las clases que ya funcionan. Si violamos OCP, tendremos que modificar constantemente clases existentes cada vez que aparece un nuevo requerimiento, lo cual es peligroso en proyectos grandes. Como dice Software Crafters, ==OCP nos obliga a diseñar clases que se puedan extender sin cambiar su código fuente==.

**Ejemplo en Python:** Imaginemos un sistema que calcula áreas de diferentes figuras. Una implementación NO OCP típica podría verse así (usando condicionales):

```python
import math

# Diseño NO OCP: AreaCalculator con if/else por tipo de figura
class AreaCalculator:
    def calculate_area(self, shape):
        # Si añadimos nuevos shapes, este método debe modificarse (no OCP)
        if isinstance(shape, Square):
            return shape.side * shape.side
        elif isinstance(shape, Circle):
            return math.pi * shape.radius * shape.radius
        else:
            raise ValueError("Figura no soportada")

class Square:
    def __init__(self, side):
        self.side = side    # Lado del cuadrado

class Circle:
    def __init__(self, radius):
        self.radius = radius  # Radio del círculo
```

En este diseño, cada vez que queremos soportar una nueva forma geométrica (por ejemplo, un `Triangle` o `Rectangle`), habría que **modificar** el método `calculate_area` de `AreaCalculator` agregando otro caso en el `if/elif`. Esto viola OCP: la clase `AreaCalculator` no está cerrada al cambio, pues debe editarse para extender el sistema.

Para cumplir OCP, reorganizamos el código usando abstracción y polimorfismo. Definimos una interfaz (clase base abstracta) común `Shape` con un método `area()`, y hacemos que cada forma implemente su propio cálculo. De este modo, la clase calculadora no necesita saber qué tipo de forma recibe: simplemente invoca el método `area` de la forma, y las clases derivadas proporcionan el comportamiento específico. Por ejemplo:

```python
from abc import ABC, abstractmethod
import math

# Diseño OCP: cada forma implementa su propio método area()
class Shape(ABC):
    @abstractmethod
    def area(self):
        pass  # Método abstracto que debe implementarse

class Square(Shape):
    def __init__(self, side):
        self.side = side  # Lado del cuadrado
    def area(self):
        # Cálculo del área del cuadrado (lado al cuadrado)
        return self.side * self.side

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius  # Radio del círculo
    def area(self):
        # Cálculo del área del círculo (pi * r^2)
        return math.pi * self.radius * self.radius

class AreaCalculator:
    def calculate_area(self, shape: Shape):
        # Gracias al polimorfismo, basta invocar shape.area()
        return shape.area()
```

En esta versión **OCP** de `AreaCalculator`, el método `calculate_area` trabaja con la abstracción `Shape` y llama a `shape.area()`. Si queremos añadir, por ejemplo, un triángulo, sólo creamos otra clase `Triangle(Shape)` con su implementación de `area()`. **No hay que modificar** el código de `AreaCalculator` ni de las demás clases. Por ejemplo:

```python
class Triangle(Shape):
    def __init__(self, base, height):
        self.base = base
        self.height = height
    def area(self):
        return 0.5 * self.base * self.height  # Área de un triángulo
```

Luego podemos usarlo sin cambios en `AreaCalculator`:

```python
square = Square(4)
circle = Circle(3)
triangle = Triangle(6, 2)

calc = AreaCalculator()
print(calc.calculate_area(square))    # Usa Square.area()
print(calc.calculate_area(circle))    # Usa Circle.area()
print(calc.calculate_area(triangle))  # Usa Triangle.area()
```

Así, OCP permite **extender** el sistema (añadiendo nuevas formas) sin **modificar** el código que ya existe. Esto es crucial en proyectos reales: por ejemplo, en un sistema e-commerce podríamos añadir nuevos tipos de promociones o métodos de pago implementando nuevas clases, sin tocar la lógica principal del checkout. Esto mantiene el software estable y minimiza riesgos al cambiar sólo lo que realmente es nuevo.

## 🏛️ Principio de Sustitución de Liskov (LSP)

**Teoría:** El principio de sustitución de Liskov (LSP) dice que ==**las subclases deben poder usarse como substitutas de sus clases base sin alterar el comportamiento correcto del programa**==. En otras palabras, si existe una clase `Base` y una clase `Derivada` que la extiende, entonces cualquier código que funcione con `Base` debería seguir funcionando si recibe un objeto de la clase `Derivada` en su lugar. Esto implica que las clases derivadas deben respetar el _contrato_ definido por la clase base: no pueden cambiar la precondición ni la poscondición de los métodos base.

==Por ejemplo, si la clase base declara un método que siempre devuelve un valor positivo, ninguna subclase debería alterarlo para devolver negativo==. Violaciones del LSP suelen provocar errores en tiempo de ejecución: el código que esperaba un comportamiento (por contrato) de la base queda sorprendido por el comportamiento distinto de la derivada. El LSP fue formulado por Barbara Liskov en 1987 y es fundamental para que la herencia sea sólida: asegura que la jerarquía de clases sea lógica y consistente.

**Ejemplo en Python:** Consideremos el ejemplo clásico de aves en el que la clase base `Bird` define un método `fly()`. Si creamos una subclase `Ostrich` (avestruz) que hereda de `Bird`, pero luego implementamos `fly()` lanzando un error porque los avestruces no vuelan, habremos violado LSP. Veamos el código:

```python
from abc import ABC, abstractmethod

# EJEMPLO NO LSP: la clase Bird define fly(), pero Ostrich no puede volar
class Bird(ABC):
    @abstractmethod
    def fly(self):
        pass  # Método que debería permitir volar a un ave

class Duck(Bird):
    def fly(self):
        print("El pato está volando")  # Duck vuela normalmente

class Ostrich(Bird):
    def fly(self):
        # PROBLEMA: los avestruces no vuelan, rompemos el contrato
        raise NotImplementedError("El avestruz no puede volar")
```

Aquí, `Ostrich` hereda de `Bird` pero su implementación de `fly()` no cumple lo que el contrato de `Bird` sugiere. Cualquier código que espere un `Bird` volador se equivocará si recibe un `Ostrich`: por ejemplo, llamar a `fly()` causará una excepción inesperada. Esto rompe LSP, porque `Ostrich` **no puede reemplazar** a `Bird` en todas partes sin cambiar el comportamiento esperado.

La solución es reconsiderar la jerarquía de clases y extraer una interfaz más apropiada. Podemos definir, por ejemplo, una clase intermedia `FlyingBird` para aves voladoras y dejar `Ostrich` como un `Bird` que simplemente no implementa el método `fly()`. De este modo, respetamos LSP: cualquier `FlyingBird` sí podrá volar, y las aves no voladoras no ofrecen ese método en su contrato. Por ejemplo:

```python
# EJEMPLO CORRECTO LSP: se separan aves voladoras de aves no voladoras
class Bird:
    pass  # Clase genérica de ave (no define fly por defecto)

class FlyingBird(Bird, ABC):
    @abstractmethod
    def fly(self):
        pass  # Sólo las aves que pueden volar implementarán este método

class Duck(FlyingBird):
    def fly(self):
        # Implementación válida de fly para el pato
        print("El pato está volando")

class Ostrich(Bird):
    # Los avestruces no tienen fly, ya no heredan de FlyingBird
    pass  # No implementa fly() y no rompe LSP
```

En este segundo diseño, `Duck` (y cualquier otra ave voladora) hereda de `FlyingBird` que garantiza tener `fly()`. `Ostrich` simplemente hereda de `Bird` genérico y no se espera que vuele. Ahora, si un código requiere un `FlyingBird`, sólo trabajará con patos, águilas, etc., pero no con avestruces. De esta manera **no rompemos el contrato**: cualquier llamada a métodos de `FlyingBird` es válida en clases derivadas de `FlyingBird`, y `Ostrich` ni siquiera es vista como un `FlyingBird`, por lo que no genera sorpresa.

**Caso práctico:** En sistemas reales, LSP impide errores sutiles. Por ejemplo, ==en un sistema bancario imaginemos una clase base `CuentaBancaria` con un método `retirar(monto)` que permite retirar hasta cierto límite. Si creamos una subclase `CuentaVIP` que altera las reglas de retiro (por ejemplo, permitiendo sobregiro excesivo), podríamos romper las expectativas del código que maneja cuentas genéricas. LSP asegura que una `CuentaVIP` siga cumpliendo las reglas básicas de `CuentaBancaria` para que cualquier servicio pueda operar con ambos tipos sin fallos inesperados==. Respetar LSP es esencial para construir jerarquías de clases coherentes.

## 🔄 Principio de Segregación de Interfaces (ISP)
**Interface Segregation Principle**

**Teoría:** El principio de segregación de interfaces (Interface Segregation Principle, ISP) propone que **los clientes no deberían verse obligados a depender de interfaces que no utilizan**. En la práctica, esto significa que ==es preferible tener muchas interfaces pequeñas y específicas que una sola interfaz general y monolítica==. Si una clase hereda o implementa una interfaz con métodos que no necesita, está asumiendo dependencias inútiles. En palabras sencillas, _“un cliente nunca debería verse forzado a implementar una interfaz que no utiliza”_. Esto evita que las clases estén innecesariamente acopladas y mejora la cohesión: cada clase implementa únicamente lo que realmente le corresponde.

**Ejemplo en Python:** Supongamos un sistema de procesos donde definimos una interfaz general `Worker` para cualquier trabajador, con métodos `work()` y `eat()`. Esto es problemático para robots, ya que ellos trabajan pero no comen. Veamos el anti-ejemplo:

```python
from abc import ABC, abstractmethod

# Diseño NO ISP: Worker fuerza métodos innecesarios en Robot
class Worker(ABC):
    @abstractmethod
    def work(self):
        pass
    @abstractmethod
    def eat(self):
        pass

class Human(Worker):
    def work(self):
        print("El humano está trabajando")
    def eat(self):
        print("El humano está comiendo")

class Robot(Worker):
    def work(self):
        print("El robot está trabajando")
    def eat(self):
        # Problema: los robots no comen, pero estamos forzados a definir eat()
        raise NotImplementedError("Los robots no necesitan comer")
```

Aquí, la clase `Robot` implementa `Worker` y debe definir `eat()`, pero como los robots no comen, no tiene sentido. Aunque se implementó (arrojando un error), esto viola ISP: el robot depende de un método que **no usa**. La solución es dividir la interfaz en partes más específicas. Por ejemplo, podemos crear una interfaz `Workable` para trabajo y otra `Feedable` para “comer”:

```python
from abc import ABC, abstractmethod

# Diseño ISP: interfaces más específicas
class Workable(ABC):
    @abstractmethod
    def work(self):
        pass

class Feedable(ABC):
    @abstractmethod
    def eat(self):
        pass

class Human(Workable, Feedable):
    def work(self):
        print("El humano está trabajando")
    def eat(self):
        print("El humano está comiendo")

class Robot(Workable):
    def work(self):
        print("El robot está trabajando")
    # Robot no implementa Feedable, ya no tiene eat() redundante
```

Ahora `Human` implementa ambas interfaces (trabaja y come), y `Robot` sólo implementa `Workable` porque realmente sólo trabaja. No se obliga a `Robot` a implementar métodos irrelevantes. Esto cumple ISP: nadie depende de métodos que no usa, reduciendo dependencias innecesarias. Gracias a esta segregación, podemos añadir nuevos tipos de trabajadores (por ejemplo, `Pet` que come pero no trabaja) simplemente implementando la combinación de interfaces que corresponda, sin tocar clases ajenas.

**Caso práctico:** ==En sistemas de software reales, ISP puede observarse en servicios o APIs==. Por ejemplo, ==una interfaz `IUsuario` con métodos `crear()`, `actualizar()`, `eliminar()` y `enviarEmail()` sería abusiva: ¿por qué un repositorio de usuarios debería conocer el envío de emails? En cambio, conviene tener una interfaz separada para funcionalidades de notificación==. Así evitamos que módulos (clientes) estén forzados a depender de funciones que no usan, lo que mejora la modularidad y facilita el testing.

## 🤝Principio de Inversión de Dependencias (DIP)
**Dependency Inversion Principle**

**Teoría:** El principio de inversión de dependencias indica que **los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones**. Es decir, en lugar de que una clase principal (alta abstracción) instancie o llame directamente a clases concretas de bajo nivel (por ejemplo, detalles de infraestructura), ambas deberían depender de una interfaz o clase abstracta común. De este modo, reducimos acoplamientos: el comportamiento de alto nivel (lógica de negocio) se desacopla de los detalles concretos (persistencia, hardware, APIs externas), permitiendo intercambiarlos sin modificar las clases de alto nivel.

En palabras simples: use interfaces o clases abstractas para las dependencias. Así, el código de negocio puede trabajar con cualquier implementación concreta (por inyección de dependencias) y no “sabe” qué detalle se usa debajo. Esto facilita enormemente las pruebas unitarias, pues podemos inyectar **mocks** o stubs en lugar de los componentes reales, acelerando pipelines de CI/CD. Además, cumplir DIP ayuda a que la aplicación sea más flexible: por ejemplo, cambiar de una base de datos a otra no requiere modificar la lógica, sólo conectar una implementación diferente.

**Ejemplo en Python:** Veamos un ejemplo simple con acceso a base de datos. Primero el anti-ejemplo (violación DIP):

```python
# DISEÑO NO DIP: UserRepository depende directamente de MySQLConnection concreto
class MySQLConnection:
    def connect(self):
        return "Conexión a MySQL establecida"

class UserRepository:
    def __init__(self):
        # Acoplamiento fuerte a la base de datos MySQL
        self.db = MySQLConnection()  

    def get_users(self):
        conn = self.db.connect()
        return []  # Imaginemos que ejecuta una consulta y devuelve usuarios
```

En este diseño, `UserRepository` (módulo de alto nivel) crea directamente un objeto `MySQLConnection` (módulo de bajo nivel). Si en el futuro queremos usar PostgreSQL o una API remota, tendríamos que modificar `UserRepository`, rompiendo OCP y acoplando fuertemente la lógica de negocio a un detalle de implementación. Esto **viola DIP**, ya que no hay abstracción intermedia.

Para cumplir DIP, introducimos una interfaz común (o clase abstracta) `DBConnection` que define los métodos necesarios (`connect` en este caso). Las conexiones concretas la implementan. `UserRepository` recibe en su constructor un objeto de tipo `DBConnection`, sin saber qué implementación exacta es. Así, `UserRepository` depende de la abstracción, no de una clase concreta.

```python
from abc import ABC, abstractmethod

# Abstracción común para la conexión
class DBConnection(ABC):
    @abstractmethod
    def connect(self):
        pass

class MySQLConnection(DBConnection):
    def connect(self):
        return "Conexión a MySQL establecida"

class PostgreSQLConnection(DBConnection):
    def connect(self):
        return "Conexión a PostgreSQL establecida"

class UserRepository:
    def __init__(self, db_connection: DBConnection):
        self.db = db_connection  # Dependencia invertida: recibe la abstracción

    def get_users(self):
        conn = self.db.connect()
        return []  # Ejecutaría una consulta, no importa qué DB sea
```

Con este diseño, cumplimos DIP. Ahora podemos crear el repositorio pasando cualquier objeto que implemente `DBConnection`. Por ejemplo:

```python
mysql_conn = MySQLConnection()
repo_mysql = UserRepository(mysql_conn)        # Inyectamos MySQL

postgres_conn = PostgreSQLConnection()
repo_postgres = UserRepository(postgres_conn)  # Inyectamos PostgreSQL
```

Ni `UserRepository` ni el código de negocio deben cambiar para soportar otra base de datos. Incluso podríamos inyectar un **mock** en pruebas unitarias usando pytest (p. ej. un stub que simule `connect()`) y así testear `UserRepository` sin depender de una base real. Este uso de interfaces y **inyección de dependencias** es un patrón clave de DIP.

**Caso práctico:** En una arquitectura de microservicios, DIP es esencial. Por ejemplo, un servicio de notificaciones puede depender de la abstracción `Messenger` en lugar de un servicio de email concreto. Así, el mismo código de notificaciones puede usar implementations de SMS, email o Slack simplemente inyectando el componente deseado, sin cambiar la lógica de negocio. Este desacoplamiento hace más fácil el desarrollo en equipo y la entrega continua (CI/CD), ya que cada componente puede probarse aisladamente con mocks (usando pytest + fixtures) y desplegarse sin afectar a otros servicios. En resumen, DIP ayuda a manejar la complejidad y a construir sistemas más robustos y flexibles.