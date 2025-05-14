
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

