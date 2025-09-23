


  ![cheatsheets-1.png (1754×1240)](https://matplotlib.org/cheatsheets/_images/cheatsheets-1.png)


```python
import matplotlib.pyplot as plt
import numpy as np
```


# Generales

## Titulo
```python
plt.title("Titulo del grafico")
```

## Label
```python
plt.xlabel("Etiqueta para el eje x")
plt.ylabel("Etiqueta para el eje y")
```

## `plt.legend()`
Muestra la leyenda en el gráfico, utilizando las etiquetas proporcionadas en los gráficos de línea y dispersión.
## `plt.show()`
Muestra el grafico en la salida estándar.

## `plt.xticks()`
Se usa para personalizar las marcas del eje $X$ en un gráfico. Se puede utilizar para
1. Especificar los valores exactos que se deben mostrar en el eje $X$
2. Cambiar las etiquetas de los valores del eje $X$ (por ejemplo, mostrar nombres en lugar de números)
3. Rotar o cambiar el formato de las etiquetas del eje $X$ para mayor claridad
## Parámetros comunes
### `label`
Etiqueta que referencia a la gráfica

## `plt.close()`
Cierra todas las figuras activas creadas por Matplotlib, liberando memoria y evitando que las visualizaciones se acumulen.

```python
# Cierra una figura especifica (fig es un objeto Figure
plt.close(fig)

# Cierra solo la ultima figura creada
plt.close()

# Cierra todas las figuras activas
plt.close('all')
```

# Tipos de gráficos
## `plt.scatter()`

Genera un grafico de dispersión.
### Parámetros
- `x, y` : arreglos de las posiciones de los datos
- `c` : Define el color de los marcadores, por ejemplo `r` para rojo.
- `marker` : Define el estilo del marcador para representar los puntos en el grafico, por ejemplo una `x`.
### Ejemplo
```python
plt.scatter(x, y, c='r', marker='x')
```

```python
x_train = np.array([1.0, 2.0])
y_train = np.array([300.0, 500.0])

# Plot the data points
plt.scatter(x_train, y_train, marker='x', c='r')
# Set the title
plt.title("Houses Prices")
# Set the y-axis label
plt.ylabel("Price (in 1000s of dollars)")
# Set the x-axis label
plt.xlabel("Size (1000 sqft)")
plt.show()
```

![[scatter example.png]]


>[!info] marker
>- puntos: '.' (punto), ',' (pixel)
>- círculos: 'o'
>- triángulos: '^' (hacia arriba), 'v' (hacia abajo), '>' (hacia derecha), '<' (hacia izquierda)
>- cuadrados: 's'
>- estrellas: '\*' (estrella), 'p' (pentágono), 'h' (hexágono), 'H' (hexágono horizontal) 
>- cruces: '+' (cruz), 'x' (equis), 'D' (diamante), 'd' (diamante delgado)

> [!info] color c
> - nombres: 'red', 'blue', 'green', 'yellow', 'purple', etc.
> - códigos hexadecimales: '#FF0000' (rojo), '#0000FF' (azul), '#00FF00' (verde), etc.



## `plt.plot()`

Genera un gráfico de líneas. Conecta puntos de datos con líneas, mostrando una tendencia o relación continua entre ellos.

- Conecta automáticamente los puntos de datos con una línea.
- Ideal para mostrar tendencias, curvas, o cualquier relación continua entre puntos.
- Toma como entrada dos arreglos o listas, uno para el eje x y otro para el eje y.


```python
import matplotlib.pyplot as plt

plt.plot(x, y, color='red', linestyle='--', marker='o', linewidth=2, label='Precio casas')
```

### Parámetros
- ``x``, ``y``: Datos para los ejes X y Y, puede ser una lista o un arreglo de NumPy.
- **fmt** : Una cadena de formato que especifica el estilo de la línea y el marcador. Es una combinación opcional de color, estilo de línea, y marcador.
	- **Componentes:**
		- **Color**: `'b'` (azul), `'g'` (verde), `'r'` (rojo), `'c'` (cian), `'m'` (magenta), `'y'` (amarillo), `'k'` (negro), `'w'` (blanco).
		- **Estilo de línea**: `'-'` (línea sólida), `'--'` (línea discontinua), `'-.'` (línea punteada), `':'` (línea de puntos).
		- **Marcador**: `'.'` (punto), `'o'` (círculo), `'x'` (x), `'+'` (cruz), `'*'` (asterisco), `'s'` (cuadrado), etc.
	- **Ejemplos**
		- `'ro'`: Puntos rojos (color `'r'` y marcador `'o'`).
		- `'g--'`: Línea verde discontinua (color `'g'` y estilo de línea `'--'`).
		- `'b-.'`: Línea azul punteada (color `'b'` y estilo de línea `'-.'`).


### Ejemplos

```python

x_train = np.array([1.0, 2.0])
y_train = np.array([300.0, 500.0])

# Plot our model prediction
plt.plot(x_train, y_train, c='b')
# Set the title
plt.title("Housing Prices")
# Set the y-axis label
plt.ylabel('Price (in 1000s of dollars)')
# Set the x-axis label
plt.xlabel('Size (1000 sqft)')
plt.legend()
plt.show()
```

![[plot example.png]]


## `ax.plot_surface()`

Se usa para crear gráficos de superficies en 3D. Se invoca desde un objeto de tipo `Axes3D` de la siguiente forma

```python
ax.plot_surface(X, Y, Z, cmap=None, color=None, edgecolor=None alpha=None, rstride=1, cstride=1, shade=True)
```


### Parámetros
- `X, Y, Z` : Matrices NumPy del mismo tamaño que representan las coordenadas de la superficie
- `cmap` : Mapa de colores (`'viridis`, `plasma`, `colorwarm`, etc.)
- `color` : Color sólido de la superficie (ignorado si `cmap` está definido).
- `edgecolor` : Color de los bordes de la malla (`k` para negro)
- `alpha` : Transparencia (`alpha=0` completamente transparente, `alpha=1` opaco).
- `rstride, cstride` : Saltos de filas y columnas para controlar la resolución.
- `shade`: Si es `True`, agrega sombreado para dar efecto de profundidad.

### Ejemplos

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Crear la figura y el objeto 3D
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

# Crear datos para X, Y y Z
X = np.linspace(-5, 5, 10)  # 10 valores en X
Y = np.linspace(-5, 5, 10)  # 10 valores en Y
X, Y = np.meshgrid(X, Y)  # Crear la malla de coordenadas
Z = X**2 + Y**2  # Función Z = X² + Y²

# Graficar la superficie
ax.plot_surface(X, Y, Z, cmap='viridis')

plt.show()
```

# Examples

```python


X_features = ['size(sqft)','bedrooms','floors','age']

# This line creates a figure (fig) and an array of subplots (ax)
# subplots() is used to create a figure and a set of subplots
# 1, 4: specifies that the plot layour should have 1 row and 4 columns of subplots
# figsize(12, 3): sets the width and height of the entire figure to 12 and 3 inches respectively
# sharey: makes all the subplots share the same y-axis scale
fig,ax=plt.subplots(1, 4, figsize=(12, 3), sharey=True)
for i in range(len(ax)):
	# scatter() a functions to create a scatter plot
    ax[i].scatter(X_train[:,i],y_train)
    # set_xlabel() set s the label for the x-axis using the corresponding feature
    # name from X_features
    ax[i].set_xlabel(X_features[i])
# Sets the label for the y-axis to "Price ..." for only the first subplot
# since they share a y-axis
ax[0].set_ylabel("Price (1000's)")

plt.show()
```


# `plt.subplots()`

Se usa para crear múltiples gráficos (subgráficos) en una misma figura. No se debe confundir con `plt.subplot()`.

```python
fig, ax = plt.subplots(nrows, ncols, figsize, sharex, sharey, constrained_layout)
```

Donde
1. `fig`  ([[#`Figure`|Figure]]) : Representa el lienzo donde se dibujan los gráficos. En una figura pueden haber varios subgráficos (ejes).
2. `ax`  ([[#`Axes`|Axes]]) :  Son los "subgráficos" dentro de la figura, donde realmente se dibujan los datos. Si se tiene varios gráficos, `ax[i]` accede a un gráfico específico.

- `nrows`, `ncols` : número de filas y columnas de subgráficos.
- `figsize` : Tamaño de la figura en pulgadas (ancho, alto).  `figsize=(10, 5)`.
- `sharex` : Comparte el eje $X$ entre los subgráficos. `sharex=True`.
- `sharey` : Igual a `sharex` para el eje $Y$.
- `constrained_layout` : Ajusta automáticamente los espacios entre gráficos. `constrained_layout=True`

## Ejemplo
Queremos comparar la evolución de precios de casas y autos en dos gráficos diferentes, pero en la misma figura. 


```python
import matplotlib.pyplot as plt
import numpy as np

# Datos
años = np.array([2018, 2019, 2020, 2021, 2022])
precios_casas = np.array([300, 350, 400, 450, 500])
precios_autos = np.array([20, 22, 24, 26, 28])

# Crear la figura y los ejes con 2 filas y 1 columna
fig, ax = plt.subplots(nrows=2, ncols=1, figsize=(8, 6), sharex=True, constrained_layout=True)

# Gráfico 1: Precios de casas
ax[0].plot(años, precios_casas, 'b-o', label="Casas")
ax[0].set_ylabel("Precio ($1000)")
ax[0].set_title("Evolución del precio de casas")
ax[0].legend()
ax[0].grid(True)

# Gráfico 2: Precios de autos
ax[1].plot(años, precios_autos, 'r-s', label="Autos")
ax[1].set_xlabel("Año")
ax[1].set_ylabel("Precio ($1000)")
ax[1].set_title("Evolución del precio de autos")
ax[1].legend()
ax[1].grid(True)

# Mostrar gráfico
plt.show()

```


# Otros

## `plt.imshow()`
Es una función utilizada para mostrar imágenes en una figura. Su propósito principal es representar datos bidimensionales en forma de imagen, ya sea una matriz de píxeles (como una imagen en escala de grises o en color) o un conjunto de valores numéricos.

```python
plt.imshow(
	X,
	cmap='plasma',
	vmin=0.2, vmax=0.8,
	aspect='equal',
	interpolation='nearest'
)
```

- `X` : es la matriz de datos a visualizar, puede ser:
	- Una matriz 2D (valores de píxeles en escala de grises).
	- Una matriz 3D con dimensiones `(rows, columns, 3)` o `(rows, columns, 4)`, que representa imágenes RGB o RGBA
- `cmap (colormap)`: Define la escala de colores para datos en escala de grises o mapas de color.
	- `gray`: escala de grises
	- `viridis` : mapa de calor predeterminado
	- `hot`, `cool`, `jet` : otros mapas de calor
- `vmin` y `vmax` : Permiten definir el rango de valores de la imagen. Cualquier valor menor a `vmin` se asigna al color más oscuro, y cualquier valor mayor a `vmax` al color más claro.
- `aspect` : Controla la relación de aspecto de la imagen.
	- `auto` : se ajusta automáticamente al tamaño de la figura.
	- `equal` : mantiene la proporción original de los píxeles.
- `interpolation`: Define cómo se interpolan los píxeles al redimensionar la imagen
	- `nearest` : sin interpolación (muestra píxeles originales)
	- `bilinear` , `bicubic`, `gaussian` : suaviza la imagen.



## `Figure`
Un objeto `Figure` representa la ventana o lienzo completo donde se dibujan los gráficos. Es el contenedor principal de todos los elementos gráficos, como ejes (`Axes`), títulos y anotaciones.

### Atributos
- `figsize` : Tamaño de la figura (ancho, alto) en pulgadas.
- `dpi` : Resolución en puntos por pulgada (DPI).
- `axes` : Lista con todos los ejes (`Axes`) dentro de la figura.

### Métodos
- `add_axes(rect)` : Añade un eje en una posición específica.
- `fig.savefig("nombre.jpg")` : Guarda la figura como imagen en un archivo (`.png`, `.pdf`, etc.).
- `fig.add_subplot(nrows, ncols, index)` : Agrega un nuevo subplot (eje) en una cuadrícula de filas y columnas.
- `cls()` : Limpia la figura.
- `fig.tight_layout()` : Ajusta los gráficos para que no se superpongan. 
- `fig.suptitle` : Agrega un título a toda la figura. `fig.suptitle('Comparación de precios)`
- `fig.set_size_inches(ancho, alto)` : Cambia el tamaño de la figura. 

**Ejemplo**

```python
import matplotlib.pyplot as plt

# Crear una figura vacía con tamaño 6x4 pulgadas
fig = plt.figure(figsize=(6, 4))

# Agregar un eje en la posición [izquierda, abajo, ancho, alto] (en porcentaje)
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])

# Dibujar algo en el eje
ax.plot([0, 1, 2], [0, 1, 4], label="Ejemplo")
ax.set_title("Ejemplo con Figure y Axes")
ax.legend()

plt.show()

```


## `Axes`
Representa un conjunto de ejes dentro de una `Figure`, es decir, el área donde realmente se dibuja el gráfico. Cada figura (`Figure`) puede contener múltiples ejes (`Axes`).

```python
import matplotlib.pyplot as plt

# Crear una figura y un eje
fig, ax = plt.subplots(figsize=(6, 4))

# Dibujar una línea en el eje
ax.plot([1, 2, 3], [1, 4, 9], marker='o', linestyle='-', color='b', label="y = x^2")

# Configurar etiquetas y título
ax.set_xlabel("Eje X")
ax.set_ylabel("Eje Y")
ax.set_title("Ejemplo con Axes")
ax.legend()

plt.show()
```

### Atributos
- `xaxis`, `yaxis` : Controlan los ejes $X$ e $Y$.
- `title` : Contiene el título del eje.
- `lines` : Lista con todas las líneas dibujadas en el eje.

### Métodos

- `plot(), scatter(), bar()`, etc. : Para dibujar un gráfico de línea, de dispersión, barras u otro.
- `set_title('Titulo')` : Agrega un título al gráfico.
- `set_xlabel('Etiqueta X')` : Etiqueta del eje $X$.
- `set_ylabel('Etiqueta Y')` : Etiqueta del eje $Y$.	
- `set_xlim([min, max])` : Define límites en el eje $X$.
- `set_ylim([min, max])` : Define límites en el eje $Y$.	
- `legend()` : Muestra la leyenda del gráfico.	
- `grid(True)` : Activa la cuadrícula del gráfico.
#### `fill_between()`
Se usa para rellenar el área entre dos curvas o entre una curva y un valor constante en el eje $Y$.

```python
Axes.fill_between(x, y1, y2=0, where=None, interpolate=False, step=None, **kwargs)
```

- `x` : Array de valores en el eje $X$
- `y1` : Array de valores en el eje $Y$ (curva superior o única si $y2$ no se especifica)
- `y2` : (opcional) Segundo conjunto de valores en Y para definir la región a rellenar. Si no se da se usa $y=0$.
- `where` : (Opcional) Una condición booleana (`True` / `False`) indicando qué partes rellanar.
- `interpolate`: (Opcional) : Si es `True` interpola los valores de $x$, cuando `where=False` cambia.
- `step` : (Opcional) Puede ser `pre`, `mid` o `post` para dar un efecto de escalón.
- `**kwargs` : Argumentos opcionales para personalizar el relleno, como `color`, `alpha` (transparencia), `label`, etc.

**Ejemplo**
```python
x = np.linspace(0, 10, 100)
y = np.sin(x)

fig, ax = plt.subplots()
ax.plot(x, y, color="blue")

# Rellenar solo donde la función es positiva
ax.fill_between(x, y, where=(y > 0), color="green", alpha=0.3)

ax.set_title("Relleno solo donde y > 0")
plt.show()

```




# Scatter plot


**With `fig, ax = plt.subplots()`**

```python
fig, ax = plt.subplots()

ax.scatter(x, y, s=None, c=None, marker=None, cmap=None, alpha=None, linewidths=None, edgecolors=None, ... )
ax.set_xlabel('label X')
ax.set_ylabel('label Y')
plt.show()
```

