

# map

La función `map` es una herramienta muy útil en Python para aplicar una función específica a cada uno de los elementos de un iterable (como una lista, tupla, etc.) y devolver un iterador que produce los resultados.

## Sintaxis

```python
map(func, iterable)
```

- **`func`**: La función que se va a aplicar a cada elemento del iterable.
- **`iterable`**: El iterable (como una lista, tupla, etc.) cuyos elementos serán procesados por `func`.

## Características

- `map` devuelve un iterador, lo que significa que los resultados no se calculan hasta que se necesiten (lazy evaluation).
- Puede convertir el iterador devuelto en una lista, tupla u otro tipo de colección si es necesario, utilizando las funciones `list()`, `tuple()`, etc.

## Ejemplos de Uso

1. **Ejemplo básico**

   Aplicar una función que duplica cada número en una lista:

   ```python
   def duplicar(x):
       return x * 2

   numeros = [1, 2, 3, 4]
   resultado = map(duplicar, numeros)

   print(list(resultado))  # Salida: [2, 4, 6, 8]
   ```

2. **Uso con una función lambda**

   Utilizar una función lambda para incrementar cada número en la lista por 1:

   ```python
   numeros = [1, 2, 3, 4]
   resultado = map(lambda x: x + 1, numeros)

   print(list(resultado))  # Salida: [2, 3, 4, 5]
   ```

3. **Formateo de números**

   Formatear una lista de números flotantes a cadenas con dos decimales:

   ```python
   numeros = [2.3456, 3.4567, 4.5678]
   resultado = map('{:.2f}'.format, numeros)

   print(list(resultado))  # Salida: ['2.35', '3.46', '4.57']
   ```

4. **Uso con múltiples iterables**

   `map` también puede aceptar múltiples iterables (deben tener la misma longitud). La función debe aceptar tantos argumentos como iterables se pasen:

   ```python
   a = [1, 2, 3]
   b = [4, 5, 6]
   resultado = map(lambda x, y: x + y, a, b)

   print(list(resultado))  # Salida: [5, 7, 9]
   ```



## Ventajas de Usar `map`

- **Claridad y Concisión**: Hace que el código sea más claro y conciso en comparación con un bucle `for`.
- **Eficiencia**: `map` es generalmente más eficiente que un bucle `for` en términos de rendimiento, especialmente cuando se usa con funciones integradas.
- **Compatibilidad con Funciones de Orden Superior**: Facilita el uso de funciones de orden superior y la programación funcional en Python.

## Desventajas

- **Legibilidad para Principiantes**: Puede ser menos legible para aquellos que no están familiarizados con la programación funcional.
- **Limitación a Funciones**: Requiere que las operaciones se puedan expresar como funciones que toman uno o más argumentos.


# Pasos por valor y referencia

En Python, los **argumentos** se pasan **por referencia** y **por valor** dependiendo del tipo de dato que estemos manipulando, lo cual puede generar algo de confusión. Voy a explicar en detalle cómo funciona este mecanismo y cómo afecta a los **objetos** y sus **atributos**.

### Argumentos por valor vs. referencia

Para entender mejor, desglosamos el comportamiento de Python en dos grandes categorías de tipos de datos:

1. **Tipos inmutables** (por valor): Números, cadenas de texto, tuplas, y otros tipos inmutables.
2. **Tipos mutables** (por referencia): Listas, diccionarios, conjuntos y, en general, cualquier objeto que puedas modificar.

#### Tipos inmutables (como enteros, strings, tuplas)

En Python, cuando pasas un tipo inmutable como argumento a una función, **parece** que se pasa por valor. Esto significa que cuando modificas ese valor dentro de la función, el valor original no se altera.

Por ejemplo:

```python
def modificar_numero(n):
    n += 10
    print("Dentro de la función:", n)

num = 5
modificar_numero(num)
print("Fuera de la función:", num)
```

**Salida:**

```
Dentro de la función: 15
Fuera de la función: 5
```

Aquí, aunque el valor de `n` se modifica dentro de la función, **el valor de `num` fuera de la función no se ve afectado**. Esto se debe a que cuando pasas un tipo inmutable, Python crea una copia del valor en la memoria para usar dentro de la función.

#### Tipos mutables (como listas, diccionarios, objetos)

En cambio, si pasas un objeto **mutable**, como una lista, diccionario o un objeto personalizado, Python pasa una **referencia** al objeto original. Esto significa que si modificas el objeto dentro de la función, los cambios afectarán al objeto fuera de la función también.

Ejemplo:

```python
def modificar_lista(lista):
    lista.append(4)
    print("Dentro de la función:", lista)

mi_lista = [1, 2, 3]
modificar_lista(mi_lista)
print("Fuera de la función:", mi_lista)
```

**Salida:**

```
Dentro de la función: [1, 2, 3, 4]
Fuera de la función: [1, 2, 3, 4]
```

En este caso, al modificar `lista` dentro de la función, la **referencia** apunta al mismo objeto en memoria que `mi_lista`, por lo que el objeto original es modificado también fuera de la función.

### Objetos y sus atributos

Los objetos en Python son siempre pasados **por referencia**. Esto significa que, cuando pasas un objeto a una función, lo que estás pasando es una **referencia** a ese objeto, no una copia del objeto. Si cambias los **atributos** de ese objeto dentro de la función, los cambios serán visibles fuera de la función porque estás modificando el objeto original.

Veamos un ejemplo con una clase en Python:

```python
class MiClase:
    def __init__(self, valor):
        self.valor = valor

def modificar_objeto(obj):
    obj.valor = 100
    print("Dentro de la función:", obj.valor)

mi_objeto = MiClase(10)
modificar_objeto(mi_objeto)
print("Fuera de la función:", mi_objeto.valor)
```

**Salida:**

```
Dentro de la función: 100
Fuera de la función: 100
```

Aquí, pasamos un objeto `mi_objeto` a la función `modificar_objeto`. La función cambia el atributo `valor` del objeto, y ese cambio se refleja fuera de la función porque el objeto es **mutable** y fue pasado por referencia.

### Detalle clave: reasignación de referencias

Es importante entender que, aunque puedes modificar el contenido de un objeto mutable desde una función, **no puedes reasignar la referencia del objeto original** de afuera de la función. Por ejemplo, si intentas reasignar el objeto por completo dentro de la función, solo estarás cambiando la referencia **dentro de la función**, y no fuera de ella.

Ejemplo:

```python
def reasignar_lista(lista):
    lista = [7, 8, 9]  # Cambia la referencia local
    print("Dentro de la función:", lista)

mi_lista = [1, 2, 3]
reasignar_lista(mi_lista)
print("Fuera de la función:", mi_lista)
```

**Salida:**

```
Dentro de la función: [7, 8, 9]
Fuera de la función: [1, 2, 3]
```

En este caso, dentro de la función `reasignar_lista`, se cambió la referencia local de `lista`, pero no afectó a `mi_lista` fuera de la función. La reasignación de la referencia solo afectó la copia local del argumento.

### Resumen

- **Tipos inmutables** (números, cadenas, tuplas): Se comportan como si se pasaran **por valor**. Al cambiar el valor dentro de la función, el original no se ve afectado.
- **Tipos mutables** (listas, diccionarios, objetos): Se pasan **por referencia**. Los cambios en los atributos u elementos dentro de la función se reflejan en el objeto original.
- **Objetos** en Python son mutables por naturaleza (aunque sus atributos pueden ser inmutables). Los cambios en sus atributos dentro de una función se reflejarán fuera de la función.
- Si reasignas la referencia de un objeto dentro de una función, solo cambia dentro del alcance local de la función, no fuera de ella.

Si necesitas más detalles o ejemplos más profundos, ¡avísame!
