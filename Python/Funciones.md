

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
