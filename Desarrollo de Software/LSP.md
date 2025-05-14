
# Principio de Sustitución de Liskov (LSP)

El **Principio de Sustitución de Liskov** (LSP, por sus siglas en inglés) es un pilar de los principios SOLID en la programación orientada a objetos. En términos sencillos, este principio afirma que _los objetos de una clase base deben poder ser reemplazados por instancias de sus subtipos sin alterar el correcto funcionamiento del programa_. Es decir, si un bloque de código opera sobre la clase `A`, debería seguir funcionando correctamente aunque reciba un objeto de cualquier clase `B` que herede de `A`. En la práctica esto implica que las subclases deben **cumplir el mismo contrato** que define la clase base: mantener las mismas precondiciones, postcondiciones e invariantes. Por ejemplo, si un método de la clase padre devuelve siempre un entero positivo, su versión en la subclase tampoco debería devolver valores inesperados o lanzar excepciones no documentadas.

Este principio es esencial para obtener jerarquías de clases robustas y fáciles de mantener. Cuando se respeta LSP, nuestro código adquiere mayor **resiliencia y extensibilidad**: podemos agregar nuevas clases derivadas con la seguridad de que el código cliente que usa la clase base no se verá afectado. También facilita la **reutilización** de componentes y el trabajo con frameworks y librerías que esperan objetos con un comportamiento consistente. En cambio, violar LSP suele degenerar en comportamientos imprevistos y **bugs difíciles de detectar**, puesto que los cambios en la subclase pueden “romper” código que suponía el comportamiento original del padre.

## Síntomas de violación del LSP

Detectar una violación de LSP no siempre es obvio a simple vista, pero existen _señales de alerta_ comunes en el diseño:

- **Sobreescritura inadecuada de métodos**: Si una subclase anula un método de la clase padre y lo implementa de forma incompatible, puede romper la sustitución. Por ejemplo, anular el método para que quede vacío (no haga nada) cuando el padre realiza trabajo esencial o cambiar el tipo de valor devuelto (devolver un entero cuando el padre devolvía un texto) viola el contrato esperado.
    
- **Lanzamiento de excepciones inesperadas**: Si la clase base no lanza excepciones, pero la subclase sí (por ejemplo, cuando recibe ciertos argumentos), el código cliente que no espera ese fallo se romperá.
    
- **Inconsistencias en invariantes**: Que la subclase tenga invariantes diferentes (por ejemplo, el caso clásico: en un `Square` se fuerza ancho=alto, pero la clase `Rectangle` los trata independientemente) puede introducir comportamientos contradictorios. Al ejecutar métodos genéricos sobre ambos tipos, notamos diferencias de resultado inesperadas.
    
- **Fallas en pruebas de la clase base**: Un indicio práctico es cuando los tests unitarios escritos para la clase padre dejan de pasar al aplicar sobre la subclase. Si un test de `Rectangle` no funciona para `Square`, es señal de que _“definitivamente Square no se comporta como Rectangle”_.
    
- **Lógica especial en el cliente**: Si el código que usa la clase base necesita diferenciar entre el tipo padre y la subclase (usando `isinstance` o condicionales especiales) para funcionar correctamente, claramente se rompió LSP. En ese caso la subclase _no se puede usar indistintamente_ con la padre, lo cual complica enormemente el mantenimiento.
    
- **Cambios propagados inesperados**: A veces no falla de inmediato, pero al violar LSP se introducen efectos colaterales sutiles en partes del código aparentemente no relacionadas, haciendo el sistema más difícil de evolucionar.
    

Un ejemplo clásico de violación es el del rectángulo y el cuadrado. Si hacemos `class Square(Rectangle)` e intentamos mantener ancho=alto en la subclase, actividades sencillas como cambiar primero el ancho y luego el alto resultan en comportamientos sorprendentes (por ejemplo, duplicar el ancho de un cuadrado duplica también el alto, lo cual rompe invariantes del usuario de `Rectangle`). En este caso concreto _la abstracción se vuelve incorrecta_: un cuadrado **no puede** comportarse exactamente como un rectángulo en todos los contextos.

## Aplicación correcta en el diseño de jerarquías

Para cumplir con LSP al diseñar clases y jerarquías, hay varias buenas prácticas:

- **Respetar el contrato de la clase base**. Esto significa mantener las mismas firmas de métodos y, sobre todo, las mismas condiciones de entrada y salida. No se debe _“restringir el dominio”_ de un método en la subclase. En otras palabras, una subclase no puede exigir condiciones más estrictas (nuevas precondiciones) que la clase padre ni relajar demasiado los resultados. De lo contrario, el código cliente que espera el comportamiento original se verá afectado. Por ejemplo, si el método base acepta un parámetro entre 1 y 100, la subclase no debería limitarlo solo a 1–50 ni cambiar el significado del resultado de forma inesperada.
    
- **No eliminar funcionalidad necesaria**. Cada método de la clase base debe seguir operativo en la subclase. No se debe anular un método para dejarlo vacío o lanzar una excepción por defecto, ya que esto **corrompería la funcionalidad heredada**. Si la subclase no puede o no quiere soportar esa operación, tal vez la herencia no sea la relación correcta.
    
- **Evitar herencias inapropiadas**. A veces un subtipo no es realmente un subtipo desde el punto de vista del comportamiento. En esos casos, es mejor usar composición o interfaces separadas. Por ejemplo, en lugar de hacer `Square` herede de `Rectangle` (lo que rompe LSP), podríamos crear una interfaz abstracta `Shape` con un método `area()` y que `Rectangle` y `Square` la implementen por separado. Así un código genérico puede usar cualquier `Shape` sin depender de relaciones rígidas de herencia.
    
- **Documentar pre/postcondiciones**. Siguiendo la idea de _design by contract_, conviene dejar claros en la documentación (o usar herramientas de contratos de código) qué invariantes esperan los métodos de cada clase. De este modo, al heredar se puede comprobar fácilmente si la subclase mantiene esas condiciones. Como señala Esposito, cumplir LSP implica **no reducir el dominio** del método al heredar.
    
- **Aplicar Interface Segregation**. En la práctica, a menudo conviene dividir las responsabilidades en interfaces o clases abstractas más específicas. Si un método de la base no tiene sentido en la subclase, quizá esa subclase debería heredar de una abstracción más pequeña o diferente. Mantener clases con alta cohesión y pocos métodos ayuda a que las subclases sólo implementen lo que realmente necesitan.
    
- **Preferir composición cuando el “ES-UN” es débil**. Si la relación semántica de herencia no es clara (un cuadrado _“no es totalmente”_ un rectángulo en términos de comportamiento), es mejor diseñar la clase derivada con un atributo que use la clase base internamente (composición) o con un diseño alternativo.
    

Si se siguen estas prácticas, las jerarquías resultantes permiten extender el sistema (añadir nuevas clases derivadas) sin romper el código existente. Además, el cumplimiento de LSP facilita el mantenimiento porque evita “sorpresas” en runtime: los usuarios de la clase base pueden confiar en que todas las subclases respetan los contratos ya establecidos.

## LSP y pruebas unitarias (mocks y stubs)

El Principio de Sustitución de Liskov tiene un impacto directo en la _testabilidad_ del código. Un diseño que cumple LSP permite **sustituir objetos reales por mocks o stubs** de manera segura sin alterar el comportamiento esperado. Esto es fundamental en pruebas unitarias: cuando una clase depende de otra, podemos inyectar un mock (un objeto falso con comportamiento controlado) porque dicho mock implementa la misma interfaz o métodos que la dependencia real. Si LSP se rompiera (por ejemplo, la clase base tiene un método que la subclase no respeta), entonces el mock podría no replicar exactamente el contrato, y los tests se volverían frágiles.

Por ejemplo, imagine que tenemos una clase `Mailer` base con método `send(email)`. En pruebas, inyectamos un _MockMailer_ que implementa `send`. Si un día heredamos `SecureMailer` que cambia `send` (p.ej. requiere parámetros adicionales o lanza excepciones distintas), el test que usa `Mailer` podría fallar inesperadamente. En cambio, si `SecureMailer` respeta LSP (hace `send` con el mismo comportamiento observable), podemos sustituirlo por un mock indistintamente. De hecho, como explican varios autores, **uno debería poder sustituir stubs y mocks sin alterar las propiedades deseables del código**.

En la práctica, respetar LSP implica también fomentar el **Uso de Dependencias por Interfaz** (Dependency Injection) y separación de responsabilidades. Si el código está bien abstraído, podemos probar cada pieza aisladamente usando mocks. Por ejemplo, una función que opera sobre una abstracción `Store` funcionará igual si le pasamos una implementación real de base de datos o un stub en memoria, siempre que ambas cumplan con la interfaz. En contraste, si la subclase introduce lógica no prevista, los tests para la superclase dejarán de ser válidos.

## LSP en frameworks (Django, Flask, etc.)

En frameworks modernos es común extender clases base provistas por la librería (vistas genéricas, modelos, middlewares). El LSP se refleja en que estas clases base esperan que nuestras subclases mantengan ciertos métodos y propiedades. Por ejemplo:

- En **Django**, las _Class-Based Views_ (CBV) definen métodos como `get()` o `post()` que deben devolver respuestas. Si una subclase personalizada omite implementarlos o cambia su firma, rompemos LSP: el enrutador de Django espera que cualquier vista derivada se comporte uniformemente. De igual forma, los _ModelAdmins_ o _FormViews_ dependen de atributos predefinidos; romper esas expectativas causará errores en runtime o en plantillas.
    
- En **Flask**, aunque el enfoque es más funcional que orientado a herencia, al usar Blueprints o clases para vistas también es importante mantener la compatibilidad esperada. Un handler de ruta personalizado debe aceptar los mismos parámetros y devolver tipos esperados.
    
- En arquitecturas **REST** o APIs con frameworks como Django REST Framework o FastAPI, frecuentemente creamos subclases de serializadores, vistas y gestores. Éstas deben respetar la interfaz de CRUD definida por el framework para ser intercambiables.
    

En resumen, aunque los ejemplos concretos pueden variar, la idea es la misma: los componentes del framework confiarán en que nuestras clases derivadas se comportan como las bases. Cumplir LSP facilita la integración sin sorpresas y permite, además, testear componentes del framework usando mocks o clases fakes que implementen las mismas interfaces.

## Ejemplo 1: Violación del LSP

A continuación se muestra un ejemplo en Python con comentarios en español donde **se viola el Principio de Sustitución de Liskov**. Tenemos una clase base `Rectangle` con métodos para establecer ancho y alto, y una subclase `Square` que intenta forzar que el ancho y el alto sean iguales. Luego, la función `change_width_height` modifica primero el ancho y luego el alto de la figura que se le pasa. Al ejecutarlo con ambas clases, se observa un comportamiento inconsistente:

```python
class Rectangle:
    """Clase Rectángulo que almacena ancho y alto por separado."""
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height
    
    def set_width(self, width: float):
        """Actualiza el ancho del rectángulo."""
        self.width = width
    
    def set_height(self, height: float):
        """Actualiza el alto del rectángulo."""
        self.height = height
    
    def area(self) -> float:
        """Calcula el área del rectángulo."""
        return self.width * self.height

class Square(Rectangle):
    """Clase Cuadrado que hereda de Rectángulo, asegurando lados iguales."""
    def __init__(self, size: float):
        super().__init__(size, size)
    
    def set_width(self, width: float):
        """En un cuadrado, ancho y alto deben ser iguales al ancho."""
        self.width = width
        self.height = width
    
    def set_height(self, height: float):
        """En un cuadrado, ancho y alto deben ser iguales al alto."""
        self.width = height
        self.height = height

def change_width_height(rect: Rectangle):
    """Modifica primero el ancho y luego el alto de la forma dada."""
    rect.set_width(10)
    rect.set_height(20)
    print(f"Después de set_width(10) y set_height(20): ancho={rect.width}, alto={rect.height}, área={rect.area()}")

# Uso con Rectángulo
print("=== Rectángulo ===")
rect = Rectangle(5, 5)
print(f"Inicial: ancho={rect.width}, alto={rect.height}, área={rect.area()}")
change_width_height(rect)

# Uso con Cuadrado
print("\n=== Cuadrado ===")
square = Square(5)
print(f"Inicial: ancho={square.width}, alto={square.height}, área={square.area()}")
change_width_height(square)
```

**Salida esperada:**

```
=== Rectángulo ===
Inicial: ancho=5, alto=5, área=25
Después de set_width(10) y set_height(20): ancho=10, alto=20, área=200

=== Cuadrado ===
Inicial: ancho=5, alto=5, área=25
Después de set_width(10) y set_height(20): ancho=20, alto=20, área=400
```

Como se observa, al usar la subclase `Square` la función `change_width_height` produce un resultado diferente: en lugar de terminar con ancho=10 y alto=20 (como en el rectángulo), el cuadrado termina con 20×20. Esto ocurre porque la herencia ha forzado a que ancho y alto cambien juntos, alterando el comportamiento que la función cliente esperaba de la clase base. En resumen, **el objeto `Square` no puede sustituir a `Rectangle` sin alterar el funcionamiento correcto del código**, violando el principio LSP. Esta violación complica el mantenimiento: si después se añaden más clases derivadas de `Rectangle`, habrá que cuidar manualmente que no introduzcan estos efectos indeseados. Además, cualquier test escrito para `Rectangle` fallaría al aplicarlo sobre `Square`, indicando precisamente este incumplimiento.

## Ejemplo 2: Aplicación correcta del LSP

En contraste, este ejemplo muestra un **diseño que sí respeta LSP**. Definimos una interfaz abstracta `Shape` con métodos genéricos (`area` y `scale`), y luego implementamos clases `Rectangle` y `Square` que cumplen ese contrato. La función `total_area` trabaja sobre la abstracción `Shape`, permitiendo usar indistintamente rectángulos, cuadrados u otros objetos que la implementen. Además se incluye un **stub** (`StubShape`) para ilustrar cómo las pruebas unitarias pueden inyectar objetos falsos que cumplen la misma interfaz.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    """Interfaz genérica para formas con métodos area() y scale()."""
    @abstractmethod
    def area(self) -> float:
        ...

    @abstractmethod
    def scale(self, factor: float):
        ...

class Rectangle(Shape):
    def __init__(self, width: float, height: float):
        self.width = width
        self.height = height

    def area(self) -> float:
        """Calcula el área del rectángulo."""
        return self.width * self.height

    def scale(self, factor: float):
        """Escala ambas dimensiones por el mismo factor."""
        self.width *= factor
        self.height *= factor

class Square(Shape):
    def __init__(self, size: float):
        self.size = size

    def area(self) -> float:
        """Calcula el área del cuadrado."""
        return self.size * self.size

    def scale(self, factor: float):
        """Escala el lado del cuadrado por el factor dado."""
        self.size *= factor

def total_area(shapes):
    """Calcula la suma de áreas de todas las formas en la lista."""
    return sum(shape.area() for shape in shapes)

# Uso con diversas formas
shapes = [Rectangle(2, 3), Square(4)]
print(f"Áreas iniciales: {[shape.area() for shape in shapes]}")
print(f"Suma de áreas: {total_area(shapes)}")
for shape in shapes:
    shape.scale(2)
print(f"Áreas tras escalar: {[shape.area() for shape in shapes]}")
print(f"Suma de áreas escaladas: {total_area(shapes)}")

# Uso con stub (por ejemplo, en tests)
class StubShape(Shape):
    """Stub de Shape para pruebas, devuelve un área fija."""
    def __init__(self, area_value):
        self._area_value = area_value
    def area(self) -> float:
        return self._area_value
    def scale(self, factor: float):
        pass  # No hace nada

dummy_shapes = [StubShape(10), StubShape(20)]
print(f"Suma de áreas de formas stub: {total_area(dummy_shapes)} (esperado 30)")
```

**Explicaciones destacadas del código**:

- Ambas clases, `Rectangle` y `Square`, implementan la interfaz `Shape` y ofrecen métodos coherentes con la misma firma. No hay sobreescrituras sorpresivas: por ejemplo, `scale` simplemente multiplica las dimensiones por el factor, sin condiciones especiales. Por tanto, **se puede usar cualquier instancia de `Shape` en la función `total_area`** sin que importe su tipo concreto. Esto cumple LSP: cada subtipo se comporta como la abstracción base (no cambia las reglas de cálculo del área).
    
- La función `total_area` trabaja agnósticamente con la interfaz `Shape`. Al recibir un `Square` en lugar de un `Rectangle`, o viceversa, siempre calculará correctamente las áreas esperadas. De hecho, al escalar las formas, la suma de áreas produce resultados coherentes (12 y 16 suben a 48 y 64, respectivamente).
    
- Para pruebas, mostramos `StubShape`, un doble de prueba que implementa `Shape` devolviendo áreas fijas. Gracias a que `StubShape` respeta la interfaz, `total_area` puede operar sobre él sin problemas. Esto refleja cómo LSP facilita la creación de mocks/stubs: podemos sustituir fácilmente la implementación real por un objeto de prueba que “se comporta igual” en lo esencial, sin romper los tests.
    
- Con este diseño, el código es más fácil de **mantener y extender**. Si mañana agregamos otra forma (por ejemplo, `Circle` implementando `Shape`), el resto del sistema (cálculo de áreas, tests, componentes de interfaz gráfica, etc.) seguirá funcionando correctamente con el nuevo subtipo. No habrá código especial ni condicionales que diferencien entre los tipos de forma, gracias al LSP.
    

En resumen, el segundo ejemplo ilustra cómo un diseño que **abarca correctamente la idea de contrato** permite construir un sistema modular y testeable. Cada clase derivada puede sustituir a la abstracción base sin sorpresas, mejorando la mantenibilidad y extensibilidad del código. Además, facilita el uso de bibliotecas de testing: por ejemplo, podemos usar objetos falsos (_stubs_) o simulados (_mocks_) que implementen `Shape` en las pruebas unitarias sin que el comportamiento general cambie, justo como describen los expertos.

**Referencias:** Las citas se basan en la definición original de LSP dada por Barbara Liskov y en diversas fuentes de diseño de software que explican las señales de violación y cómo aplicar correctamente el principio. Estos principios están ampliamente documentados en materiales de SOLID y diseño orientado a objetos, y se reflejan en prácticas comunes de frameworks modernos.