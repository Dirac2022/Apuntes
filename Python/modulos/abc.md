
## Introducción

El módulo `abc` (Abstract Base Classes) en Python permite definir **clases base abstractas** que sirven como plantillas para otras clases. Estas clases pueden definir métodos abstractos que **deben ser implementados** por cualquier subclase concreta. Esto es útil para garantizar que ciertas clases sigan una interfaz común, mejorando la robustez y mantenibilidad del código.

## Conceptos clave

- **Clase abstracta**: No puede instanciarse directamente. Sirve como base para otras clases.
- **Método abstracto**: Método declarado pero sin implementación. Obliga a las subclases a implementarlo.
- **Metaclase `ABCMeta`**: Controla la creación de clases abstractas.
- **Decorador `@abstractmethod`**: Marca un método como abstracto.

## Explicación

- **`ABC`** es una clase base que tiene como metaclase `ABCMeta`. Al heredar de `ABC`, tu clase se convierte en abstracta.
- **`@abstractmethod`** marca un método que no tiene implementación en la clase base y que debe ser implementado en cualquier subclase concreta.
- Si una subclase no implementa todos los métodos abstractos, no podrá instanciarse.

## Ventajas del uso de `abc`

- **Contratos claros**: Define interfaces explícitas para tus clases.
- **Prevención de errores**: Evita instanciar clases incompletas.
- **Polimorfismo seguro**: Garantiza que todas las subclases tengan ciertos métodos.
- Facilita el diseño orientado a interfaces.

## Importación básica

```python
from abc import ABC, abstractmethod
```

- `ABC`: Clase base que facilita la creación de clases abstractas.
- `abstractmethod`: Decorador para declarar métodos abstractos.

## Ejemplo 1: Clase abstracta simple con métodos abstractos

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    """Clase abstracta que define la interfaz para animales."""

    @abstractmethod
    def make_sound(self):
        """Método abstracto que debe ser implementado para emitir el sonido del animal."""
        pass

    @abstractmethod
    def move(self):
        """Método abstracto que debe ser implementado para definir el movimiento del animal."""
        pass

# Intentar crear una instancia de Animal dará error:
# animal = Animal()  # TypeError: Can't instantiate abstract class Animal with abstract methods make_sound, move

```

## Ejemplo 2: Clases concretas que implementan la clase abstracta

```python
class Dog(Animal):
    def make_sound(self):
        return "Woof!"

    def move(self):
        return "Runs"

class Bird(Animal):
    def make_sound(self):
        return "Chirp!"

    def move(self):
        return "Flies"

# Uso:
dog = Dog()
print(dog.make_sound())  # Woof!
print(dog.move())        # Runs

bird = Bird()
print(bird.make_sound())  # Chirp!
print(bird.move())        # Flies

```

## Ejemplo 3: Método abstracto con implementación parcial (métodos concretos dentro de clase abstracta)

```python
class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

    def stop_engine(self):
        print("Engine stopped.")

class Car(Vehicle):
    def start_engine(self):
        print("Car engine started.")

car = Car()
car.start_engine()  # Car engine started.
car.stop_engine()   # Engine stopped.

```

## Ejemplo 4: Propiedades abstractas

Puedes definir propiedades abstractas que deben ser implementadas en las subclases.

```python
class Person(ABC):
    @property
    @abstractmethod
    def name(self):
        """Nombre de la persona (propiedad abstracta)."""
        pass

class Student(Person):
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name

student = Student("Ana")
print(student.name)  # Ana

```

## Ejemplo 5: Uso avanzado con múltiples métodos abstractos y herencia múltiple

```python
class Logger(ABC):
    @abstractmethod
    def log(self, message):
        pass

class FileLogger(Logger):
    def log(self, message):
        with open("log.txt", "a") as f:
            f.write(message + "\n")

class ConsoleLogger(Logger):
    def log(self, message):
        print(message)

def process_data(logger: Logger):
    logger.log("Processing started")
    # Procesamiento...
    logger.log("Processing finished")

# Uso:
console_logger = ConsoleLogger()
process_data(console_logger)

file_logger = FileLogger()
process_data(file_logger)

```


## Ejemplo completo con documentación y uso de `abc`

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """
    Clase abstracta que representa una figura geométrica.
    Todas las figuras deben implementar los métodos area() y perimeter().
    """

    @abstractmethod
    def area(self):
        """
        Calcula el área de la figura.
        Debe ser implementado por las subclases.
        """
        pass

    @abstractmethod
    def perimeter(self):
        """
        Calcula el perímetro de la figura.
        Debe ser implementado por las subclases.
        """
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        import math
        return math.pi * self.radius ** 2

    def perimeter(self):
        import math
        return 2 * math.pi * self.radius

# Uso
shapes = [Rectangle(3, 4), Circle(5)]
for shape in shapes:
    print(f"Área: {shape.area():.2f}, Perímetro: {shape.perimeter():.2f}")

```

## Resumen

|Concepto|Descripción|
|---|---|
|`ABC`|Clase base para definir clases abstractas.|
|`abstractmethod`|Decorador para declarar métodos que deben implementarse en subclases.|
|Clase abstracta|No puede instanciarse directamente; sirve como plantilla para subclases.|
