
# `await`
Es una palabra clave en Python que se utiliza para pausar la ejecución de una función asíncrona hasta que la corutina o la promesa que sigue sea completada.



# Decorador
Un **decorador** en Python es una función que envuelve a otra función o método para extender o modificar su comportamiento sin cambiar su código fuente. Se representa con el símbolo `@` seguido del nombre del decorador y se coloca encima de la definición de la función o método.


# Regla LEGB

La regla **LEGB** es un conjunto de prioridades que Python sigue para buscar y resolver variables en diferentes ámbitos. Esta regla ayuda a Python a determinar **de dónde proviene una variable** y **cuál valor debe usar**.

---

### **¿Qué significa LEGB?**

La sigla LEGB describe los **niveles de búsqueda** para las variables en Python, en el siguiente orden:

1. **Local (L)**: Variables definidas dentro de la función o el bloque actual.
2. **Enclosing (E)**: Variables de funciones externas que envuelven (funciones anidadas).
3. **Global (G)**: Variables definidas en el ámbito global del módulo.
4. **Built-in (B)**: Variables predefinidas por Python (como `len`, `print`, etc.).

Python buscará una variable en este orden. Si no encuentra la variable en ninguno de los niveles, lanza un error `NameError`.

---

### **Explicación de Cada Nivel**

#### **1. Local (L)**

Es el ámbito más cercano, dentro de la función o bloque donde se ejecuta el código.

- Si una variable se declara o se pasa como parámetro en una función, es **local**.
- Python usará la variable local antes de buscar en niveles superiores.

**Ejemplo**:

```python
def funcion():
    x = 10  # Variable local
    print(x)

funcion()  # Imprime: 10
```

---

#### **2. Enclosing (E)**

Es el ámbito de **funciones externas** que envuelven a una función anidada. Este nivel solo se aplica si las funciones están anidadas.

**Ejemplo**:

```python
def externa():
    x = 20  # Variable en el ámbito "enclosing"
    
    def interna():
        print(x)  # Busca en "enclosing"
    
    interna()

externa()  # Imprime: 20
```

---

#### **3. Global (G)**

Son las variables definidas en el nivel más alto del módulo, fuera de todas las funciones. Estas variables están disponibles para cualquier función dentro del mismo archivo, a menos que una función las sobrescriba.

**Ejemplo**:

```python
x = 30  # Variable global

def funcion():
    print(x)  # Busca en "global"

funcion()  # Imprime: 30
```

> Si necesitas modificar una variable global dentro de una función, debes usar la palabra clave `global`.

---

#### **4. Built-in (B)**

Python tiene un conjunto de variables y funciones integradas que están disponibles automáticamente, como `len`, `print`, `range`, etc. Este es el último nivel donde Python busca una variable.

**Ejemplo**:

```python
print(len([1, 2, 3]))  # len es una función predefinida en el ámbito built-in
```

Si creas una variable o función con el mismo nombre que una built-in, la sobrescribes en niveles superiores.

**Ejemplo**:

```python
len = 10  # Sobrescribe la función built-in
print(len)  # Imprime: 10
```

---

### **Orden de Búsqueda LEGB**

|Nivel|Dónde se busca|Ejemplo de variable|
|---|---|---|
|**Local**|Dentro de la función o bloque actual.|Parámetros de la función o variables locales.|
|**Enclosing**|En la función externa que envuelve la función actual.|Variables de funciones anidadas.|
|**Global**|Variables declaradas en el módulo.|Variables fuera de funciones.|
|**Built-in**|Variables integradas de Python.|Funciones como `len`, `print`, etc.|

---

### **Ejemplo Completo del Flujo LEGB**

```python
x = 50  # Variable global

def externa():
    x = 40  # Enclosing

    def interna():
        x = 30  # Local
        print(x)  # Busca en LEGB: Local -> Enclosing -> Global -> Built-in

    interna()

externa()  # Imprime: 30
```

---

### **Errores Típicos**

Si Python no encuentra la variable en ninguno de los niveles, lanza un `NameError`.

**Ejemplo**:

```python
def funcion():
    print(x)  # Error porque x no está definida en ningún nivel LEGB

funcion()  # NameError: name 'x' is not defined
```




# `@property`

Imagina que estás creando una clase simple en Python, por ejemplo, para un `Producto`. En un principio, podrías hacer esto:


```python
class Producto:
    def __init__(self, nombre, precio):
        self.nombre = nombre
        self.precio = precio

# Creamos una instancia y accedemos a sus atributos directamente
tele = Producto("Televisor 4K", 1500)
print(f"El precio del {tele.nombre} es ${tele.precio}") # >> El precio del Televisor 4K es $1500

# El problema: cualquiera puede asignar un valor inválido
tele.precio = -50
print(f"Nuevo precio: ${tele.precio}") # >> Nuevo precio: $-50
```

El problema es evidente: no tenemos **ningún control** sobre el valor que se le asigna a `precio`. Un precio negativo no tiene sentido, pero nuestra clase lo permite sin quejarse.

#### La Solución "Clásica" (Estilo Java/C++): Getters y Setters

Una forma de solucionar esto es ocultar el atributo (usando un guion bajo `_` por convención) y crear métodos para obtener (get) y establecer (set) su valor.

```python
class Producto:
    def __init__(self, nombre, precio):
        self.nombre = nombre
        self._precio = precio  # Atributo "privado" por convención

    def get_precio(self):
        return self._precio

    def set_precio(self, nuevo_precio):
        if nuevo_precio < 0:
            print("Error: El precio no puede ser negativo.")
        else:
            self._precio = nuevo_precio

tele = Producto("Televisor 4K", 1500)
tele.set_precio(-50) # >> Error: El precio no puede ser negativo.
print(tele.get_precio()) # >> 1500
```

Esto funciona, pero tiene una gran desventaja: **es poco "Pythonico"**. Rompe la simplicidad del acceso directo. Ahora, en lugar de `tele.precio`, tienes que usar `tele.get_precio()` y `tele.set_precio()`. Si tuvieras un código grande que ya usaba `tele.precio`, tendrías que refactorizarlo todo.

#### La Solución Elegante y "Pythonica": `@property`

Aquí es donde brilla el decorador `@property`. **Te permite exponer un método como si fuera un atributo.** Te da lo mejor de ambos mundos:

- **La sintaxis limpia y directa** de un atributo público (`tele.precio`).
- **El control y la lógica de validación** de los métodos getter y setter.

Con `@property`, puedes empezar con un atributo público simple y, si más adelante necesitas añadir lógica (como la validación), puedes hacerlo sin cambiar la forma en que el resto del código interactúa con tu clase.

---

### Una Clase Completa: `Circulo`

El ejemplo de un círculo es perfecto para ver todo el poder de `@property`, incluyendo atributos calculados.


```python
import math

class Circulo:
    """
    Una clase para representar un círculo, demostrando el uso de @property.
    El atributo principal es el radio, a partir del cual se calculan los demás.
    """
    def __init__(self, radio):
        # La validación inicial ocurre en el constructor.
        # Usamos el 'setter' que definiremos más abajo para no repetir código.
        self.radio = radio

    @property
    def radio(self):
        """Este es el 'getter' para el radio.
        Se ejecuta cuando accedemos a 'circulo.radio'.
        Devuelve el valor del atributo interno _radio.
        """
        print("(Llamando al getter de radio)")
        return self._radio

    @radio.setter
    def radio(self, nuevo_radio):
        """Este es el 'setter' para el radio.
        Se ejecuta cuando asignamos un valor: 'circulo.radio = valor'.
        Contiene la lógica de validación.
        """
        print(f"(Llamando al setter de radio con el valor {nuevo_radio})")
        if nuevo_radio <= 0:
            raise ValueError("El radio debe ser un número positivo.")
        # El valor real se almacena en un atributo "privado"
        self._radio = nuevo_radio

    @property
    def diametro(self):
        """Este es un 'atributo calculado' de solo lectura (getter).
        No almacenamos el diámetro, lo calculamos al momento.
        Se accede con 'circulo.diametro'.
        """
        print("(Calculando diámetro...)")
        return self._radio * 2

    @diametro.setter
    def diametro(self, nuevo_diametro):
        """También podemos crear un setter para un atributo calculado.
        Si alguien modifica el diámetro, en realidad estamos cambiando el radio.
        """
        print(f"(Llamando al setter de diámetro con el valor {nuevo_diametro})")
        self._radio = nuevo_diametro / 2

    @property
    def area(self):
        """Este es un atributo de SOLO LECTURA.
        Como solo definimos el @property (getter) y NO un .setter,
        intentar asignar un valor a 'circulo.area' dará un error.
        """
        print("(Calculando área...)")
        return math.pi * self._radio ** 2
```

**Uso Práctico de la Clase `Circulo`**

```python
print("--- Creando el círculo ---")
c = Circulo(10)

print("\n--- Accediendo al radio (getter) ---")
print(f"El radio es: {c.radio}")

print("\n--- Modificando el radio (setter) ---")
c.radio = 12
print(f"El nuevo radio es: {c.radio}")

print("\n--- Accediendo al diámetro (atributo calculado) ---")
print(f"El diámetro es: {c.diametro}")

print("\n--- Modificando el diámetro (setter de atributo calculado) ---")
c.diametro = 30
print(f"El nuevo diámetro es: {c.diametro}")
print(f"El radio ahora se ha actualizado a: {c.radio}") # ¡Se actualizó automáticamente!

print("\n--- Accediendo al área (atributo de solo lectura) ---")
print(f"El área es: {c.area:.2f}") # Formateado a 2 decimales

print("\n--- Intentando asignar un valor inválido ---")
try:
    c.radio = -5
except ValueError as e:
    print(f"Error capturado: {e}")

print("\n--- Intentando modificar un atributo de solo lectura ---")
try:
    c.area = 999
except AttributeError as e:
    print(f"Error capturado: {e}")
```

### Resumen de la Magia de `@property`:

1. **Getter (`@property`):** Define un método que se ejecuta al _leer_ el atributo. Permite cálculos sobre la marcha.
    
2. **Setter (`@nombre.setter`):** Define un método que se ejecuta al _asignar_ un valor al atributo. Ideal para validaciones.
    
3. **Atributo de Solo Lectura:** Si solo defines el `@property` (getter) y no el setter, el atributo no se puede modificar, lo que es útil para valores que no deben cambiar, como un ID o un área calculada.
    
4. **Código Limpio:** Mantiene la interfaz de tu clase simple y directa, ocultando la lógica compleja detrás de un acceso que parece un atributo normal.