

# Operador `@`
Está diseñado para realizar **multiplicación de matrices** de forma más explícita y eficiente. Este operador simplifica la sintaxis para operaciones que involucran multiplicación matricial, siendo equivalente a la función `numpy.matmul()` o `numpy.dot()` en muchos casos.

### Multiplicación de matrices con `@`:
El operador `@` es útil cuando trabajas con matrices o vectores, especialmente en álgebra lineal, ya que permite realizar la multiplicación de matrices de una forma más concisa y fácil de leer. Vamos a ver cómo funciona.

**Ejemplo**
```python
import numpy as np

# Definir dos matrices
A = np.array([[1, 2],
              [3, 4]])

B = np.array([[5, 6],
              [7, 8]])

# Multiplicación matricial con el operador @
C = A @ B
print(C)
```

**Resultado**
```python
[[19 22]
 [43 50]]
```


### Similitudes con las funciones de NumPy:

El operador `@` está diseñado principalmente para la multiplicación de matrices, y su comportamiento es equivalente a ciertas funciones de `NumPy`:

| Función de NumPy           | Descripción                                                                                   | Equivalente al operador `@` |
| -------------------------- | --------------------------------------------------------------------------------------------- | --------------------------- |
| `numpy.dot()`              | Realiza producto escalar entre vectores, o producto matricial entre dos matrices.             | En el caso de matrices, sí. |
| `numpy.matmul()`           | Realiza multiplicación de matrices (2D), pero puede manejar arrays de dimensiones superiores. | Sí, es equivalente.         |

### Casos en los que podrías usar `@`:

1. **Multiplicación de matrices 2D**:
   El caso más directo y frecuente es multiplicar matrices 2D. Usar `@` te permite evitar llamadas más largas a funciones como `numpy.dot()` o `numpy.matmul()`, haciéndolo más legible.

   ```python
   C = A @ B  # Multiplicación de matrices
   ```

2. **Producto escalar de vectores**:
   Aunque `@` no es directamente equivalente a `np.dot()` para vectores (pues `np.dot()` hace el producto escalar para 1D), puedes usarlo para productos de vectores 1D interpretados como matrices 1xN o Nx1. Veamos un ejemplo:

   ```python
   v1 = np.array([1, 2])
   v2 = np.array([3, 4])

   result = v1 @ v2  # Producto escalar
   print(result)
   ```

   El resultado es el mismo que con `np.dot(v1, v2)`.

### Diferencias entre `@` y las funciones de NumPy:

- **Compatibilidad con dimensiones superiores**:
   El operador `@` y `numpy.matmul()` funcionan de manera similar para matrices 2D, pero en el caso de arrays de más dimensiones, `numpy.matmul()` puede manejar mejor la multiplicación de tensores. El operador `@` también soporta esta funcionalidad con NumPy.

   ```python
   # Array 3D
   A = np.random.rand(2, 2, 2)
   B = np.random.rand(2, 2, 2)

   # Matmul para tensores 3D
   C = np.matmul(A, B)
   ```

- **Múltiples matrices**:
   `numpy.linalg.multi_dot()` puede multiplicar más de dos matrices a la vez, optimizando el orden de las operaciones para reducir la cantidad de multiplicaciones. El operador `@` no es capaz de hacer esto directamente.

   ```python
   # Múltiples matrices
   C = np.linalg.multi_dot([A, B, A])
   ```

### Comparativa de rendimiento:
En operaciones con grandes matrices o muchas operaciones, usar el operador `@` puede ser más eficiente que llamar repetidamente a `numpy.dot()` o `numpy.matmul()` debido a que es más directo y está optimizado para la multiplicación de matrices.

