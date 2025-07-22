
## `deque`

La clase `deque` (double-ended queue) del módulo `collections` en Python proporciona una estructura de datos similar a una lista, pero con la ventaja de que las operaciones de añadir y eliminar elementos desde ambos extremos (izquierda y derecha) son eficientes en tiempo O(1). Esto la hace ideal para implementar colas (FIFO) y pilas (LIFO), así como otras estructuras donde se requiere una inserción y eliminación eficiente en los extremos.

Aquí tienes una exploración de los métodos más comunes y cómo usarlos:

**Creación de un `deque`:**

```python
from collections import deque

# Crea un deque vacío
d = deque()
print(d)  # Output: deque([])

# Crea un deque con elementos iniciales de un iterable (lista, tupla, string, etc.)
mi_lista = [1, 2, 3]
d = deque(mi_lista)
print(d)  # Output: deque([1, 2, 3])

mi_string = "abc"
d = deque(mi_string)
print(d)  # Output: deque(['a', 'b', 'c'])

# Crea un deque con una longitud máxima (los elementos se eliminan del extremo opuesto al añadir si se alcanza el límite)
d = deque(maxlen=3)
d.append(1)
d.append(2)
d.append(3)
print(d)  # Output: deque([1, 2, 3], maxlen=3)
d.append(4)
print(d)  # Output: deque([2, 3, 4], maxlen=3)
```

**Añadir elementos:**

- `append(x)`: Añade `x` al extremo derecho del deque.
- `appendleft(x)`: Añade `x` al extremo izquierdo del deque.
- `extend(iterable)`: Extiende el extremo derecho del deque añadiendo todos los elementos del `iterable`.
- `extendleft(iterable)`: Extiende el extremo izquierdo del deque añadiendo todos los elementos del `iterable`. Nota: los elementos se añaden de forma que el último elemento del iterable se convierte en el primer elemento del deque.

Python

```python
d = deque([1, 2])
d.append(3)
print(d)  # Output: deque([1, 2, 3])

d.appendleft(0)
print(d)  # Output: deque([0, 1, 2, 3])

d.extend([4, 5])
print(d)  # Output: deque([0, 1, 2, 3, 4, 5])

d.extendleft([-1, -2])
print(d)  # Output: deque([-2, -1, 0, 1, 2, 3, 4, 5])
```

**Eliminar elementos:**

- `pop()`: Elimina y devuelve un elemento del extremo derecho del deque. Si el deque está vacío, levanta una excepción `IndexError`.
- `popleft()`: Elimina y devuelve un elemento del extremo izquierdo del deque. Si el deque está vacío, levanta una excepción `IndexError`.
- `remove(value)`: Elimina la primera aparición de `value`. Si no se encuentra, levanta una excepción `ValueError`.
- `clear()`: Elimina todos los elementos del deque, dejándolo con una longitud de 0.

Python

```python
d = deque([1, 2, 3, 2, 4])
print(d.pop())     # Output: 4
print(d)           # Output: deque([1, 2, 3, 2])

print(d.popleft())  # Output: 1
print(d)           # Output: deque([2, 3, 2])

d.remove(2)
print(d)           # Output: deque([3, 2])

d.clear()
print(d)           # Output: deque([])
```

**Otros métodos útiles:**

- `count(x)`: Devuelve el número de ocurrencias de `x` en el deque.
- `rotate(n=1)`: Rota los elementos del deque `n` pasos hacia la derecha. Si `n` es negativo, la rotación es hacia la izquierda. Si el deque no está vacío, una rotación de un paso a la derecha es equivalente a `d.appendleft(d.pop())`, y una rotación de un paso a la izquierda es equivalente a `d.append(d.popleft())`.
- `reverse()`: Invierte el orden de los elementos en el deque in-place y devuelve `None`.
- `maxlen`: Atributo de solo lectura que devuelve la longitud máxima del deque si se especificó al crearlo, o `None` si no tiene límite.

Python

```python
d = deque([1, 2, 2, 3, 2])
print(d.count(2))  # Output: 3

d.rotate(2)
print(d)          # Output: deque([3, 2, 1, 2, 2])

d.rotate(-1)
print(d)          # Output: deque([2, 3, 2, 1, 2])

d.reverse()
print(d)          # Output: deque([2, 1, 2, 3, 2])

d_con_max_len = deque([1, 2, 3], maxlen=3)
print(d_con_max_len.maxlen)  # Output: 3
```

**Uso como Cola (FIFO):**

Python

```python
cola = deque()
cola.append(1)  # Encolar
cola.append(2)
cola.append(3)

print(cola.popleft())  # Desencolar (devuelve 1)
print(cola)           # Output: deque([2, 3])
```

**Uso como Pila (LIFO):**

Python

```python
pila = deque()
pila.append(1)  # Apilar
pila.append(2)
pila.append(3)

print(pila.pop())  # Desapilar (devuelve 3)
print(pila)        # Output: deque([1, 2])
```
