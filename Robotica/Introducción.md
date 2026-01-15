
## Vectores

Declarar un vector en numpy
```python
import numpy as np
vector = np.array([1, 2, 3, 4, 5])
print(vector)
# [1 2 3 4 5]
```

Declarar un vector en sympy
```python
import sympy as sp

# Declara las variables simbólicas
x, y, z = sp.symbols("x y z")

# Declara un vector columna
vector = sp.Matrix([x, y, z])

# Para declarar un vector fila
# sp.Matrix([[x, y, z]])
print(vector)
# Matrix([[x], [y], [z]])
```

<h6>Transpuesta de un vector</h6>
Transpuesta de un vector en numpy

```python
import numpy as np
vector = np.array([1, 2, 3, 4, 5])
matrix_columna = vector.reshape(-1, 1)
matrix_fila = vector.reshape(1, -1)
print("Vector:", vector)
print("Matrix columna:", matrix_columna)
print("Matrix fila:", matrix_fila)
# Vector: [1 2 3 4 5]
# Matrix columna: [[1] [2] [3] [4] [5]]
# Matrix fila: [[1 2 3 4 5]]
```


Transpuesta en sympy
```python
import sympy as sp

# Definir los símbolos
x, y, z = sp.symbols("x y z")

# Crear el vector como una matriz columna
vector = sp.Matrix([x, y, z])
print(f"Matriz columna: \n{vector}")

# Obtener la transpuesta del vector
vector_T = vector.T
print(f"Matriz fila: \n{vector_T}")

# Matriz columna: 
# Matrix([[x], [y], [z]])
# Matriz fila: 
# Matrix([[x, y, z]])
```

<h5>Producto escalar</h5>

Producto escalar en numpy

```python
import numpy as np
v1 = np.array([1, 2, 3])
v2 = np.array([4, 5, 6])
dot_producto = np.dot(v1, v2)
print(dot_producto)
# 32
```

Producto escalar en sympy

```python
# Definir los simbolos para los componentes de los vectores
x1, y1, z1 = sp.symbols('x1 y1 z1')
x2, y2, z2 = sp.symbols('x2 y2 z2')

# Crear los vectores como matrices columna
v1 = sp.Matrix([x1, y1, z1])
v2 = sp.Matrix([x2, y2, z2])

# Calcular el producto escalar
dot_producto = v1.dot(v2)
print(dot_producto)
# x1*x2 + y1*y2 + z1*z2

# Reemplazar los símbolos con valores numéricos
valores = {x1: 1, y1:2, z1:3, x2:4, y2:5, z2:6}
# valores = [(x1, 1), (y1, 2), (z1, 3), (x2, 4), (y2, 5), (z2, 6)]
# valores = [[x1, 1], [y1, 2], [z1, 3], [x2, 4], [y2, 5], [z2, 6]]
dot_producto_evaluado = dot_producto.subs(valores)
print(dot_producto_evaluado)
```

<h5>Norma de un vector</h5>

Norma en numpy

```python
import numpy as np
vector = np.array([1, 2, 3])
norma = np.linalg.norm(vector)
print("La norma del vector es:", norma)
# La norma del vector es: 3.7416573867739413
```

En SymPy

```python
import sympy as sp

# Declara las variables simbólicas
x, y, z = sp.symbols("x y z")

# Define el vector
vector = sp.Matrix([x, y, z])

# Calcula la norma simbólica del vector
norma_simb = vector.norm()

# Sustituye los valores en el vector
vector_substituido = vector.subs({x:1, y:2, z:3})

# Calcula la norma del vector con los valores sustituidos
norma_num = vector_substituido.norm()

# Evaluar el resultado numerico
norma_num_evaluado = norma_num.evalf()

print(f"La norma simbolica del vector es : {norma_simb}")
print(f"El vector sustituido es : {vector_substituido}")
print(f"La norma del vector sustituido es : {norma_num}")
print(f"La norma del vector sustituido como numero es : {norma_num_evaluado}")
# La norma simbólica del vector es: sqrt(Abs(x)**2 + Abs(y)**2 + Abs(z)**2)
# El vector sustituido es: Matrix([[1], [2], [3]])
# La norma del vector sustituido es: sqrt(14)
# La norma del vector sustituido como número es: 3.74165738677394
```

<h5>Producto vectorial</h5>

Producto vectorial en numpy

```python
import numpy as np

# Define los dos vectores
vector1 = np.array([1, np.sqrt(2), 3])
vector2 = np.array([4, 5, 6])

# Calcula el producto vectorial
producto_vectorial = np.cross(vector1, vector2)

# Redondea el resultado a dos decimales
producto_vectorial_redondeado = np.round(producto_vectorial, 2)

print(f"El producto vectorial de {vector1} y {vector2} es: \n{producto_vectorial_redondeado}")

# El producto vectorial de [1. 1.41421356 3. ] y [4 5 6] es: 
# [-6.51 6. -0.66]
```

Producto vectorial en sympy

```python
import sympy as sp

# Define las variables simbolicas
x1, y1, z1 = sp.symbols("x1 y1 z1")
x2, y2, z2 = sp.symbols("x2 y2 z2")

# Define los dos vectores
vector1 = sp.Matrix([x1, y1, z1])
vector2 = sp.Matrix([x2, y2, z2])

# Calcula el producto vectorial simbolico
producto_vectorial = vector1.cross(vector2)

# Sustituye los valores en los vectores
vector1_subs = vector1.subs({x1:1, y1:sp.sqrt(2), z1:3})
vector2_subs = vector2.subs({x2:4, y2:5, z2:6})

# Calcula el producto vectorial con los valores sustituidos
producto_vectorial_subs = vector1_subs.cross(vector2_subs)

# Evalua el resultado numerico a dos decimales
producto_vectorial_evaluado = producto_vectorial_subs.evalf(2)

print(f"El producto vectorial simbólico es: {producto_vectorial}")
print(f"El producto vectorial con valores sustituidos es: {producto_vectorial_subs}")
print(f"El producto vectorial evaluado y redondeado a 2 decimales es: {producto_vectorial_evaluado}")

# El producto vectorial simbólico es: Matrix([[y1*z2 - y2*z1], [-x1*z2 + x2*z1], [x1*y2 - x2*y1]]) 
# El producto vectorial con valores sustituidos es: Matrix([[-15 + 6*sqrt(2)], [6], [5 - 4*sqrt(2)]]) 
# El producto vectorial evaluado y redondeado a 2 decimales es: Matrix([[-6.5], [6.0], [-0.66]])
```

<h5>Producto exterior</h5>

$$
xy^{T} =
\begin{bmatrix}
x_1y_1 & x_1y_2 & \cdots & x_1y_n \\
x_2y_1 & x_2y_2 & \cdots & x_2y_n \\
\vdots & \vdots & \ddots & \vdots \\
x_ny_1 & x_ny_2 & \cdots & x_ny_n
\end{bmatrix}

$$

Producto exterior en numpy

```python
import numpy as np

# Define los dos vectores
vector1 = np.array([1, 2, 3])
vector2 = np.array([4, 5, 6])

# Calcula el producto exterior
producto_exterior = np.outer(vector1, vector2)
print(f"El producto exterior de {vector1} y {vector2}, es:\n{producto_exterior}")
```

```
El producto exterior de [1 2 3] y [4 5 6], es:
[[ 4  5  6]
 [ 8 10 12]
 [12 15 18]]
```

Producto exterior en sympy

```python
import sympy as sp

# Definir los simbolos para los componentes de los vectores
x1, y1, z1 = sp.symbols('x1 y1 z1')
x2, y2, z2 = sp.symbols('x2 y2 z2')

# Crear los vectores como matrices columna
vector1 = sp.Matrix([x1, y1, z1])
vector2 = sp.Matrix([x2, y2, z2])

# Calcula el producto exterior
producto_exterior = vector1 * vector2.T
print(f"El producto exterior simbolico es: {producto_exterior}")

# Sustituye los valores en los vectores
# Sustituye los valores en los vectores
vector1_subs = vector1.subs({x1:1, y1:2, z1:3})
vector2_subs = vector2.subs({x2:4, y2:5, z2:6})

# Evalua el producto exterior con los valores sustituidos
producto_exterior_evaluado = vector1_subs * vector2_subs.T
print(f"El producto exterior evaluado con  valores es: \n{producto_exterior_evaluado}")
```


```
El producto exterior simbolico es: Matrix([[x1*x2, x1*y2, x1*z2], [x2*y1, y1*y2, y1*z2], [x2*z1, y2*z1, z1*z2]])
El producto exterior evaluado con  valores es: 
Matrix([[4, 5, 6], [8, 10, 12], [12, 15, 18]])
```

<h5>Triple producto escalar</h5>

Triple producto escalar en numpy
```python
import numpy as np
a = np.array([1, 4, 7])
b = np.array([8, 2, 5])
c = np.array([6, 9, 3])
producto_vectorial = np.cross(b, c)
triple_producto_escalar = np.dot(a, producto_vectorial)
print(f"El triple producto escalar es: {triple_producto_escalar}")
# El triple producto escalar es: 405
```

Triple producto escalar en sympy
```python
import sympy as sp
a1, a2, a3 = sp.symbols('a1 a2 a3')
b1, b2, b3 = sp.symbols('b1 b2 b3')
c1, c2, c3 = sp.symbols('c1 c2 c3')
a = sp.Matrix([a1, a2, a3])
b = sp.Matrix([b1, b2, b3])
c = sp.Matrix([c1, c2, c3])
producto_vectorial = b.cross(c)
triple_producto_escalar = a.dot(producto_vectorial)
valores = {a1: 1, a2: 4, a3: 7, b1: 8, b2: 2, b3: 5, c1: 6, c2: 9, c3: 3}
triple_producto_escalar_numérico = triple_producto_escalar.subs(valores)
print("Resultado simbólico del triple producto escalar:", triple_producto_escalar)
print("Resultado numérico del triple producto escalar:", triple_producto_escalar_numérico)
# Resultado simbólico del triple producto escalar: a1*(b2*c3 - b3*c2) + a2*(-b1*c3 + b3*c1) + a3*(b1*c2 - b2*c1)
# Resultado numérico del triple producto escalar: 405
```

## Diferenciación de vectores

Derivada de un vector en sympy
```python
import sympy as sp
t = sp.symbols('t')
f_t = sp.Matrix([sp.sin(t), sp.cos(t), t**2])
df_dt = f_t.diff(t)
valor_t = 2
df_dt_numerico = df_dt.subs(t, valor_t)
df_dt_numerico = df_dt_numerico.evalf()
df_dt_numerico = sp.Matrix([sp.N(x, 2) for x in df_dt_numerico])
print("Derivada simbólica del vector f(t) respecto a t:", df_dt)
print(f"Derivada del vector f(t) en t = {valor_t}:", df_dt_numerico)
# Derivada simbólica del vector f(t) respecto a t: Matrix([[cos(t)], [-sin(t)], [2*t]])
# Derivada del vector f(t) en t = 2: Matrix([[-0.42], [-0.91], [4.0]])
```

<h5>Derivada del producto escalar</h5>

Derivada del producto escalar en sympy

```python
import sympy as sp
t = sp.symbols('t')
f_t = sp.Matrix([sp.sin(t), sp.cos(t), t**2])
g_t = sp.Matrix([sp.exp(t), t, sp.log(t + 1)])
producto_escalar = f_t.dot(g_t)
derivada_producto_escalar = sp.diff(producto_escalar, t)
valor_t = 2
derivada_numérica = derivada_producto_escalar.subs(t, valor_t)
derivada_numérica_redondeada = sp.N(derivada_numérica, 2)
print("Derivada simbólica del producto escalar de f(t) y g(t) respecto a t:", derivada_producto_escalar)
print(f"Derivada del producto escalar en t = {valor_t}:", derivada_numérica_redondeada)
# Derivada simbólica del producto escalar de f(t) y g(t) respecto a t: t**2/(t + 1) + 2*t*log(t + 1) - t*sin(t) + exp(t)*sin(t) + exp(t)*cos(t) + cos(t)
# Derivada del producto escalar en t = 2: 7.1
```

<h5>Derivada del producto vectorial</h5>

Derivada del producto vectorial en sympy

```python
import sympy as sp
t = sp.symbols('t')
f_t = sp.Matrix([sp.sin(t), sp.cos(t), t**2])
g_t = sp.Matrix([sp.exp(t), t, sp.log(t + 1)])
producto_vectorial = f_t.cross(g_t)
derivada_producto_vectorial = producto_vectorial.diff(t)
t_val = 2
valores_numericos = {t: t_val}
derivada_producto_vectorial_numerico = derivada_producto_vectorial.subs(valores_numericos)
derivada_producto_vectorial_numerico_redondeado = [sp.N(val, 2) for val in derivada_producto_vectorial_numerico]
print("Producto vectorial simbólico:", producto_vectorial)
print("Derivada del producto vectorial simbólica:", derivada_producto_vectorial)
print("Derivada del producto vectorial numérica (redondeada a 2 decimales):", derivada_producto_vectorial_numerico_redondeado)
# Producto vectorial simbólico: Matrix([[-t**3 + log(t + 1)*cos(t)], [t**2*exp(t) - log(t + 1)*sin(t)], [t*sin(t) - exp(t)*cos(t)]])
# Derivada del producto vectorial simbólica: Matrix([[-3*t**2 - log(t + 1)*sin(t) + cos(t)/(t + 1)], [t**2*exp(t) + 2*t*exp(t) - log(t + 1)*cos(t) - sin(t)/(t + 1)], [t*cos(t) + exp(t)*sin(t) - exp(t)*cos(t) + sin(t)]])
# Derivada del producto vectorial numérica (redondeada a 2 decimales): [-13., 59., 9.9]
```

<h5>Gradiente de una función escalar</h5>

Gradiente en sympy

```python
import sympy as sp
x, y = sp.symbols('x y')
f = 2*x**3 + y**4
variables = sp.Matrix([x, y])
gradiente = sp.Matrix([sp.diff(f, var) for var in variables])
punto = {x: 1, y: 2}
gradiente_en_punto = gradiente.subs(punto)
print("Función escalar:", f)
print("Gradiente simbólico:", gradiente)
print("Gradiente en el punto (1, 2):", gradiente_en_punto)
# Función escalar: 2*x**3 + y**4
# Gradiente simbólico: Matrix([[6*x**2], [4*y**3]])
# Gradiente en el punto (1, 2): Matrix([[6], [32]])
```

<h5>Proyección de un vector sobre otro</h5>

Proyección en numpy

```python
import numpy as np
a = np.array([3, 4])
b = np.array([1, 2])
producto_escalar = np.dot(a, b)
norma_b = np.linalg.norm(b)
proyeccion = (producto_escalar / norma_b**2) * b
print("Vector a:", a)
print("Vector b:", b)
print("Proyección de a sobre b:", proyeccion)
# Vector a: [3 4]
# Vector b: [1 2]
# Proyección de a sobre b: [2.2 4.4]
```

Proyección en sympy

```python
import sympy as sp
x, y = sp.symbols('x y')
u, v = sp.symbols('u v')
a = sp.Matrix([x, y])
b = sp.Matrix([u, v])
producto_escalar = a.dot(b)
norma_b = b.norm()
proyeccion_simbólica = (producto_escalar / norma_b**2) * b
valores = {x: 3, y: 4, u: 1, v: 2}
proyeccion_numérica = proyeccion_simbólica.subs(valores)
proyeccion_numérica_redondeada = [sp.N(comp, 2) for comp in proyeccion_numérica]
print("Vector simbólico a:", a)
print("Vector simbólico b:", b)
print("Proyección simbólica de a sobre b:", proyeccion_simbólica)
print("Proyección numérica de a sobre b con a = [3, 4] y b = [1, 2]:", proyeccion_numérica_redondeada)
# Vector simbólico a: Matrix([[x], [y]])
# Vector simbólico b: Matrix([[u], [v]])
# Proyección simbólica de a sobre b: Matrix([[u*(u*x + v*y)/(Abs(u)**2 + Abs(v)**2)], [v*(u*x + v*y)/(Abs(u)**2 + Abs(v)**2)]])
# Proyección numérica de a sobre b con a = [3, 4] y b = [1, 2]: [2.2, 4.4]
```


## Matrices


Declarar una matriz en numpy

```python
import numpy as np
matriz = np.array([[1, 2, 3], [4, 5, 6]])
print("Matriz:", matriz)
print("Dimensiones de la matriz:", matriz.shape)
# Matriz: [[1 2 3] [4 5 6]]
# Dimensiones de la matriz: (2, 3)
```

Declarar una matriz en sympy

```python
import sympy as sp
a, b, c, d, e, f = sp.symbols("a b c d e f")
matriz = sp.Matrix([[a, b, c], [d, e, f]])
print("Matriz:", matriz)
print("Dimensiones de la matriz:", matriz.shape)
# Matriz: Matrix([[a, b, c], [d, e, f]])
# Dimensiones de la matriz: (2, 3)
```

<h5>Transpuesta de una matriz</h5>

Transpuesta en numpy
```python
import numpy as np
matriz = np.array([[1, 2, 3], [4, 5, 6]])
matriz_transpuesta = matriz.T
print("Matriz original:", matriz)
print("Matriz transpuesta:", matriz_transpuesta)
# Matriz original: [[1 2 3] [4 5 6]]
# Matriz transpuesta: [[1 4] [2 5] [3 6]]
```

Transpuesta en sympy

```python
import sympy as sp
a, b, c, d = sp.symbols('a b c d')
matriz = sp.Matrix([[a, b], [c, d]])
matriz_transpuesta = matriz.T
print("Matriz original:", matriz)
print("Matriz transpuesta:", matriz_transpuesta)
# Matriz original: Matrix([[a, b], [c, d]])
# Matriz transpuesta: Matrix([[a, c], [b, d]])
```

<h5>Matriz triangular superior e inferior</h5>

Matriz triangular en numpy

```python
import numpy as np
matriz = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
matriz_triang_sup = np.triu(matriz)
matriz_triang_inf = np.tril(matriz)
print("Matriz original:", matriz)
print("Matriz triangular superior:", matriz_triang_sup)
print("Matriz triangular inferior:", matriz_triang_inf)
# Matriz original: [[1 2 3] [4 5 6] [7 8 9]]
# Matriz triangular superior: [[1 2 3] [0 5 6] [0 0 9]]
# Matriz triangular inferior: [[1 0 0] [4 5 0] [7 8 9]]
```

Matriz triangular en sympy

```python
import sympy as sp
a, b, c, d, e, f, g, h, i = sp.symbols('a b c d e f g h i')
matriz = sp.Matrix([[a, b, c], [d, e, f], [g, h, i]])
matriz_triang_sup = matriz.upper_triangular()
matriz_triang_inf = matriz.lower_triangular()
print("Matriz original:")
sp.pprint(matriz)
print("Matriz triangular superior:")
sp.pprint(matriz_triang_sup)
print("Matriz triangular inferior:")
sp.pprint(matriz_triang_inf)
# Matriz original:
# [a  b  c]
# [d  e  f]
# [g  h  i]
# Matriz triangular superior:
# [a  b  c]
# [0  e  f]
# [0  0  i]
# Matriz triangular inferior:
# [a  0  0]
# [d  e  0]
# [g  h  i]
```

<h5>Matriz diagonal</h5>

Matriz diagonal en numpy

```python
import numpy as np
diagonal = np.diag([1, 2, 3])
print("Matriz Diagonal:", diagonal)
# Matriz Diagonal: [[1 0 0] [0 2 0] [0 0 3]]
```

Matriz diagonal en sympy

```python
import sympy as sp
a, b, c = sp.symbols('a b c')
matriz_diagonal = sp.diag(a, b, c)
print("Matriz Diagonal:")
sp.pprint(matriz_diagonal)
# Matriz Diagonal:
# [a  0  0]
# [0  b  0]
# [0  0  c]
```

<h5>Matriz identidad</h5>

Matriz identidad en numpy

```python
import numpy as np
matriz_identidad = np.eye(4)
print("Matriz Identidad:", matriz_identidad)
# Matriz Identidad: [[1. 0. 0. 0.] [0. 1. 0. 0.] [0. 0. 1. 0.] [0. 0. 0. 1.]]
```

<h5>Matriz identidad en sympy</h5>

```python
import sympy as sp
matriz_identidad = sp.eye(4)
print("Matriz Identidad:")
sp.pprint(matriz_identidad)
# Matriz Identidad:
# [1  0  0  0]
# [0  1  0  0]
# [0  0  1  0]
# [0  0  0  1]
```

<h5>Igualdad de matrices</h5>

Igualdad en numpy

```python
import numpy as np
matrix1 = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
matrix2 = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
son_iguales = np.array_equal(matrix1, matrix2)
son_iguales_elementos = matrix1 == matrix2
print("¿Son las matrices iguales?:", son_iguales)
print("¿Los elementos son iguales?:", son_iguales_elementos)
# ¿Son las matrices iguales?: True
# ¿Los elementos son iguales?: [[ True True True] [ True True True] [ True True True]]
```

Igualdad en sympy

```python
import sympy as sp
matrix1 = sp.Matrix([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
matrix2 = sp.Matrix([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
son_iguales = matrix1 == matrix2
print("¿Son las matrices iguales?:", son_iguales)
# ¿Son las matrices iguales?: True
```


<h5>Multiplicación de Matrices</h5>

Multiplicación en numpy

```python
import numpy as np
matrix1 = np.array([[1, 2, 3], [4, 5, 6]])
matrix2 = np.array([[7, 8], [9, 10], [11, 12]])
producto_matrices = np.dot(matrix1, matrix2)
print("Producto de las matrices:", producto_matrices)
# Producto de las matrices: [[ 58 64] [139 154]]
```

Multiplicación en sympy

```python
import sympy as sp
a, b, c, d, e, f, g, h = sp.symbols('a b c d e f g h')
matrix1 = sp.Matrix([[a, b], [c, d]])
matrix2 = sp.Matrix([[e, f], [g, h]])
producto_matrices = matrix1 * matrix2
valores = {a: 1, b: 2, c: 3, d: 4, e: 5, f: 6, g: 7, h: 8}
producto_matrices_evaluado = producto_matrices.subs(valores)
print("Producto de las matrices simbólicas:")
sp.pprint(producto_matrices)
print("Producto de las matrices evaluado numéricamente:", producto_matrices_evaluado)
# Producto de las matrices simbólicas:
# [a*e + b*g  a*f + b*h]
# [c*e + d*g  c*f + d*h]
# Producto de las matrices evaluado numéricamente: Matrix([[19, 22], [43, 50]])
```

<h5>Traza de una matriz</h5>

Traza en numpy

```python
import numpy as np
matriz = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
traza = np.trace(matriz)
print("Matriz:", matriz)
print("Traza de la matriz:", traza)
# Matriz: [[1 2 3] [4 5 6] [7 8 9]]
# Traza de la matriz: 15
```

Traza en sympy

```python
import sympy as sp
a, b, c, d, e, f, g, h, i = sp.symbols("a b c d e f g h i")
matriz = sp.Matrix([[a, b, c], [d, e, f], [g, h, i]])
traza = matriz.trace()
print("Matriz simbólica:")
sp.pprint(matriz)
print("Traza de la matriz simbólica:", traza)
# Matriz simbólica:
# [a  b  c]
# [d  e  f]
# [g  h  i]
# Traza de la matriz simbólica: a + e + i
```

<h5>Determinante de una matriz</h5>

Determinante en numpy

```python
import numpy as np
matriz = np.array([[1, 4, 6], [7, 2, 5], [9, 8, 3]])
determinante = np.linalg.det(matriz)
print("Matriz:", matriz)
print("Determinante de la matriz:", round(determinante, 2))
# Matriz: [[1 4 6] [7 2 5] [9 8 3]]
# Determinante de la matriz: 290.0
```

Determinante en sympy

```python
import sympy as sp
a, b, c, d, e, f, g, h, i = sp.symbols('a b c d e f g h i')
matriz = sp.Matrix([[a, b, c], [d, e, f], [g, h, i]])
determinante = matriz.det()
print("Matriz simbólica:")
sp.pprint(matriz)
print("Determinante de la matriz simbólica:", determinante)
# Matriz simbólica:
# [a  b  c]
# [d  e  f]
# [g  h  i]
# Determinante de la matriz simbólica: a*e*i - a*f*h - b*d*i + b*f*g + c*d*h - c*e*g
```

<h5>Norma de una matriz</h5>

Norma en numpy

```python
import numpy as np
A = np.array([[1, 2, 3], [4, 5, 6]])
norma_frobenius = np.linalg.norm(A)
print("Norma de Frobenius:", norma_frobenius)
# Norma de Frobenius: 9.539392014169456
```

Norma en sympy

```python
import sympy as sp
a, b, c, d, e, f = sp.symbols('a b c d e f')
A = sp.Matrix([[a, b, c], [d, e, f]])
norma_frobenius_simbólica = A.norm('fro')
valores = {a: 1, b: 2, c: 3, d: 4, e: 5, f: 6}
norma_frobenius_numérica = norma_frobenius_simbólica.subs(valores).evalf()
print("Norma de Frobenius (simbólica):", norma_frobenius_simbólica)
print("Norma de Frobenius (numérica):", norma_frobenius_numérica)
# Norma de Frobenius (simbólica): sqrt(Abs(a)**2 + Abs(b)**2 + Abs(c)**2 + Abs(d)**2 + Abs(e)**2 + Abs(f)**2)
# Norma de Frobenius (numérica): 9.53939201416946
```

<h5>Inversa de una matriz</h5>

Inversa en numpy

```python
import numpy as np
matriz = np.array([[1, 2], [3, 4]])
inversa = np.linalg.inv(matriz)
producto = np.dot(matriz, inversa)
print("Matriz:", matriz)
print("Matriz inversa:", inversa)
print("Demostración:", np.round(producto, 2))
# Matriz: [[1 2] [3 4]]
# Matriz inversa: [[-2. 1.] [ 1.5 -0.5]]
# Demostración: [[1. 0.] [0. 1.]]
```

Inversa en sympy

```python
import sympy as sp
a, b, c, d = sp.symbols('a b c d')
matriz = sp.Matrix([[a, b], [c, d]])
inversa_simbolica = matriz.inv()
valores = {a: 1, b: 2, c: 3, d: 4}
matriz_numerica = matriz.subs(valores)
inversa_numerica = inversa_simbolica.subs(valores)
producto_simbolico = matriz * inversa_simbolica
producto_numerico = matriz_numerica * inversa_numerica
print("Matrix simbólica:")
sp.pprint(matriz)
print("Matrix inversa simbólica:")
sp.pprint(inversa_simbolica)
print("Demostración simbólica:")
sp.pprint(producto_simbolico)
print("Matrix numerica:")
sp.pprint(matriz_numerica)
print("Matrix inversa numerica:")
sp.pprint(inversa_numerica)
print("Demostración numerica:")
sp.pprint(producto_numerico)
# Matrix simbólica:
# [a  b]
# [c  d]
# Matrix inversa simbólica:
# [ d/(a*d - b*c)  -b/(a*d - b*c)]
# [-c/(a*d - b*c)   a/(a*d - b*c)]
# Demostración simbólica:
# [1  0]
# [0  1]
# Matrix numerica:
# [1  2]
# [3  4]
# Matrix inversa numerica:
# [ -2   1]
# [3/2 -1/2]
# Demostración numerica:
# [1  0]
# [0  1]
```

<h5>Exponencial de una matriz</h5>

Exponencial en numpy (usando scipy)

```python
import numpy as np
import scipy.linalg as la
matriz = np.array([[1, 2], [3, 4]])
exponencial = la.expm(matriz)
print("Matriz:", matriz)
print("Exponencial de la matriz:", exponencial)
# Matriz: [[1 2] [3 4]]
# Exponencial de la matriz: [[ 51.9689562  74.73656457] [112.10484685 164.07380305]]
```

<h5>Exponencial en sympy</h5>

```python
import sympy as sp
A = sp.Matrix([[1, 2], [3, 4]])
exp_A = A.exp().evalf()
print("Matriz:")
sp.pprint(A)
print("Exponencial de la matriz:")
sp.pprint(exp_A)
# Matriz:
# [1  2]
# [3  4]
# Exponencial de la matriz:
# [51.9689561987050  74.7365645670032]
# [112.104846850505  164.073803049210]
```

Exponencial simbólica en sympy

```python
import sympy as sp
a, b, c, d = sp.symbols('a b c d')
A = sp.Matrix([[a, b], [c, d]])
exp_A_simbolico = A.exp()
valores = {a: 1, b: 2, c: 3, d: 4}
exp_A_numerico = exp_A_simbolico.subs(valores).evalf()
print("Matriz original simbólica:", A)
print("Exponencial simbólica de la matriz:", exp_A_simbolico)
print("Exponencial de la matriz con valores numéricos:", exp_A_numerico)
# (Salida simbólica extensa, se omite por brevedad)
```

<h5>Diferenciación de una matriz</h5>

Derivada de una matriz en sympy

```python
import sympy as sp
t = sp.symbols('t')
A = sp.Matrix([[t**2, sp.sin(t)], [sp.exp(t), t]])
A_derivada = A.diff(t)
valor_t = 2
A_derivada_numerica = A_derivada.subs(t, valor_t).evalf()
print("Matriz original:")
sp.pprint(A)
print("Matriz derivada respecto al tiempo:")
sp.pprint(A_derivada)
print("Matriz derivada con t = 2:")
sp.pprint(A_derivada_numerica)
# Matriz original:
# [ t**2  sin(t)]
# [exp(t)     t]
# Matriz derivada respecto al tiempo:
# [    2*t   cos(t)]
# [exp(t)      1]
# Matriz derivada con t = 2:
# [4.0  -0.416146836547142]
# [7.38905609893065  1.0]
```

<h5>Derivada de la inversa de una matriz</h5>

Derivada de la inversa en sympy

```python
import sympy as sp
t = sp.symbols('t')
A = sp.Matrix([[t, sp.sin(t)], [sp.exp(t), t**2]])
A_inv = A.inv()
A_derivada = A.diff(t)
A_inv_derivada = -A_inv * A_derivada * A_inv
t_val = 1
A_inv_derivada_numerica = A_inv_derivada.subs(t, t_val).evalf()
print("Inversa de la matriz:", A_inv)
print("Derivada simbólica de la inversa de la matriz:", A_inv_derivada)
print("Derivada de la inversa de la matriz con t = 1:", A_inv_derivada_numerica)
# (Salida simbólica extensa, se omite por brevedad)
```

<h5>El Jacobiano</h5>

Jacobiano en sympy

```python
import sympy as sp
x, y, z = sp.symbols('x y z')
F = sp.Matrix([x**2 * y, y**2, sp.sin(x)*z])
variables = sp.Matrix([x, y, z])
J = F.jacobian(variables)
valores = {x: 1, y: 2, z: 3}
J_numerico = J.subs(valores).evalf()
print("Jacobiano simbólico:")
sp.pprint(J)
print("Jacobiano numérico con x=1, y=2, z=3:")
sp.pprint(J_numerico)
# Jacobiano simbólico:
# [2*x*y  x**2  0]
# [  0    2*y   0]
# [z*cos(x)  0  sin(x)]
# Jacobiano numérico con x=1, y=2, z=3:
# [4.0  1.0  0]
# [0    4.0  0]
# [1.62090691760442  0  0.841470984807897]
```

## La función arctan

<h5>arctan en numpy</h5>
```python
import numpy as np
y = 1
angulo = np.arctan(y)
print("Ángulo (en radianes) para arctan:", angulo)
print("Ángulo (en grados) para arctan:", np.degrees(angulo))
# Ángulo (en radianes) para arctan: 0.7853981633974483
# Ángulo (en grados) para arctan: 45.0
```

<h5>atan en sympy</h5>

```python
import sympy as sp
y = sp.Symbol('y')
angulo_simb = sp.atan(y)
angulo_val = angulo_simb.subs(y, 1)
angulo_degrees = sp.deg(angulo_val)
print("Ángulo simbólico para atan(y):", angulo_simb)
print("Ángulo (en radianes) para atan(1):", angulo_val)
print("Ángulo (en grados) para atan(1):", sp.N(angulo_degrees, 4))
# Ángulo simbólico para atan(y): atan(y)
# Ángulo (en radianes) para atan(1): pi/4
# Ángulo (en grados) para atan(1): 45.00
```

<h5>La función arctan2</h5>

### arctan2 en numpy
```python
import numpy as np
y, x = 1, 1
angulo = np.arctan2(y, x)
print("Ángulo (en grados) para arctan2(y, x):", np.degrees(angulo))
y, x = 1, -1
angulo = np.arctan2(y, x)
print("Ángulo (en grados) para arctan2(y, x):", np.degrees(angulo))
y, x = -1, -1
angulo = np.arctan2(y, x)
print("Ángulo (en grados) para arctan2(y, x):", np.degrees(angulo))
y, x = -1, 1
angulo = np.arctan2(y, x)
print("Ángulo (en grados) para arctan2(y, x):", np.degrees(angulo))
# Ángulo (en grados) para arctan2(y, x): 45.0
# Ángulo (en grados) para arctan2(y, x): 135.0
# Ángulo (en grados) para arctan2(y, x): -135.0
# Ángulo (en grados) para arctan2(y, x): -45.0
```

### atan2 en sympy

```python
import sympy as sp
x, y = sp.symbols('x y')
angulo_simb = sp.atan2(y, x)
angulo_val = angulo_simb.subs({y: 1, x: -1})
angulo_degrees = sp.deg(angulo_val)
print("Ángulo simbólico para atan2(y, x):", angulo_simb)
print("Ángulo (en radianes) para atan2(1, -1):", angulo_val)
print("Ángulo (en grados) para atan2(1, -1):", sp.N(angulo_degrees, 5))
# Ángulo simbólico para atan2(y, x): atan2(y, x)
# Ángulo (en radianes) para atan2(1, -1): 3*pi/4
# Ángulo (en grados) para atan2(1, -1): 135.00
```

## Integral indefinida

### Integral indefinida en sympy
```python
import sympy as sp
x = sp.symbols("x")
f = (sp.sin(x)**2 * sp.cos(x)**2) / (sp.sin(x)**4 + sp.cos(x)**4)
integral = sp.integrate(f, x)
valor_reemplazo = sp.pi / 4
integral_evaluada = integral.subs(x, valor_reemplazo).evalf()
print("La función es:", f)
print("La integral es:", integral)
print("La integral evaluada en x=", valor_reemplazo, "es:", integral_evaluada)
# La función es: sin(x)**2*cos(x)**2/(sin(x)**4 + cos(x)**4)
# La integral es: -x/2 + sqrt(2)*atan(sqrt(2)*tan(x) - 1)/4 + sqrt(2)*atan(sqrt(2)*tan(x) + 1)/4
# La integral evaluada en x= pi/4 es: 0.162661285571072
```

## Integral doble indefinida

### Integral doble indefinida en sympy
```python
import sympy as sp
x, y = sp.symbols('x y')
f = x / (x + y)
integral_dy_dx = sp.integrate(sp.integrate(f, y), x)
integral_dx_dy = sp.integrate(sp.integrate(f, x), y)
valores = {x: 1, y: 2}
integral_dy_dx_numerica = integral_dy_dx.subs(valores).evalf()
integral_dx_dy_numerica = integral_dx_dy.subs(valores).evalf()
print("Integral doble indefinida con respecto a y y luego x (simbólica):")
sp.pprint(integral_dy_dx)
print("Integral doble indefinida con respecto a x y luego y (simbólica):")
sp.pprint(integral_dx_dy)
print("Resultado de la integral doble con respecto a y y luego x, con x=1 y y=2:", integral_dy_dx_numerica)
print("Resultado de la integral doble con respecto a x y luego y, con x=1 y y=2:", integral_dx_dy_numerica)
# (Salida simbólica extensa, se omite por brevedad)
```

## Integral definida

### Integral definida en sympy
```python
import sympy as sp
x = sp.symbols('x')
f = x**2
integral_definida = sp.integrate(f, (x, 0, 1))
resultado_numerico = integral_definida.evalf()
print("Resultado numérico de la integral definida:", resultado_numerico)
# Resultado numérico de la integral definida: 0.333333333333333
```

## Integral doble definida

### Integral doble definida en sympy
```python
import sympy as sp
x, y = sp.symbols('x y')
f = x**2 + y**2
integral_doble = sp.integrate(sp.integrate(f, (y, 0, 2)), (x, 0, 1))
resultado_numerico = integral_doble.evalf()
print("Resultado numérico de la integral doble definida:", resultado_numerico)
# Resultado numérico de la integral doble definida: 3.33333333333333
```

### Integral doble definida (infinito) en sympy
```python
import sympy as sp
x, y = sp.symbols('x y')
f = sp.exp(-(x**2 + y**2))
integral_doble = sp.integrate(sp.integrate(f, (y, -sp.oo, sp.oo)), (x, -sp.oo, sp.oo))
resultado_numerico = integral_doble.evalf()
print("Resultado simbólico de la integral doble definida:", integral_doble)
print("Resultado numérico de la integral doble definida:", resultado_numerico)
# Resultado simbólico de la integral doble definida: pi
# Resultado numérico de la integral doble definida: 3.14159265358979
```

### Integral doble definida (límites variables) en sympy
```python
import sympy as sp
x, y = sp.symbols("x y")
f = x
integral_doble = sp.integrate(sp.integrate(f, (y, 4*x/3, sp.sqrt(25 - x**2))), (x, 0, 3))
resultado_numerico = integral_doble.evalf()
print("La función es:", f)
print("La integral definida es:", integral_doble)
print("Resultado numérico de la integral definida:", resultado_numerico)
# La función es: x
# La integral definida es: 25/3
# Resultado numérico de la integral definida: 8.33333333333333
```

## Gráfica de una función

### Gráfica de seno y coseno
```python
import matplotlib.pyplot as plt
import numpy as np
t = np.linspace(0, 10, 15)
f1 = np.sin(t)
f2 = np.cos(t)
plt.figure(figsize=(10,5))
plt.plot(t, f1, label="seno")
plt.plot(t, f2, marker="d", linestyle=":", color="red", label="coseno")
plt.legend()
plt.title("Funciones")
plt.xlabel("Eje t")
plt.ylabel("Eje f(t)")
plt.grid(True)
plt.show()
```

## Gráfica de una trayectoria 2D

### Trayectoria paramétrica
```python
import numpy as np
import matplotlib.pyplot as plt
t = np.linspace(0, 2 * np.pi, 100)
x = np.cos(t)
y = np.sin(t)
plt.figure(figsize=(6,6))
plt.plot(x, y)
plt.xlabel('x(t)')
plt.ylabel('y(t)')
plt.title('Trayectoria de una partícula en función del tiempo')
plt.grid(True)
plt.axis('equal')
plt.show()
```

### Trayectoria explícita
```python
import numpy as np
import matplotlib.pyplot as plt
x = np.linspace(-1, 1, 400)
y_pos = np.sqrt(1 - x**2)
y_neg = -np.sqrt(1 - x**2)
plt.figure(figsize=(6,6))
plt.plot(x, y_pos, label='y = sqrt(1 - x^2)')
plt.plot(x, y_neg, label='y = -sqrt(1 - x^2)')
plt.xlabel('x')
plt.ylabel('y')
plt.title('Trayectoria de una partícula y versus x')
plt.grid(True)
plt.axis('equal')
plt.legend()
plt.show()
```

## Gráfica de una trayectoria 3D

### Trayectoria 3D
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
t = np.linspace(0, 10, 100)
x = np.cos(t)
y = np.sin(t)
z = t
fig = plt.figure(figsize=(10,8))
ax = fig.add_subplot(111, projection='3d')
ax.plot(x, y, z, label='Trayectoria helicoidal', color='b')
ax.set_xlabel('X(t)')
ax.set_ylabel('Y(t)')
ax.set_zlabel('Z(t)')
ax.set_title('Trayectoria 3D de una partícula')
ax.legend()
plt.show()
```
