```python
import matplotlib.pyplot as plt
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

## Parámetros comunes
### `label`
Etiqueta que referencia a la gráfica


# Tipos de gráficos
## Grafico de dispersión

`plt.scatter` genera un grafico de dispersión.
### Parámetros
- `x, y` : arreglos de las posiciones de los datos
- `c` : Define el color de los marcadores, por ejemplo `r` para rojo.
- `marker` : Define el estilo del marcador para representar los puntos en el grafico, por ejemplo una `x`.
### Ejemplo
```python
plt.scatter(x, y, c='r', marker='x')
```

## Gráficos de líneas

`plt.plot()` conecta puntos de datos con líneas, mostrando una tendencia o relación continua entre ellos.

- Conecta automáticamente los puntos de datos con una línea.
- Ideal para mostrar tendencias, curvas, o cualquier relación continua entre puntos.
- Toma como entrada dos arreglos o listas, uno para el eje x y otro para el eje y.

### Parámetros
- **x**, **y**: Datos para los ejes X y Y, puede ser una lista o un arreglo de NumPy.
- **fmt** : Una cadena de formato que especifica el estilo de la línea y el marcador. Es una combinación opcional de color, estilo de línea, y marcador.
	- **Componentes:**
		- **Color**: `'b'` (azul), `'g'` (verde), `'r'` (rojo), `'c'` (cian), `'m'` (magenta), `'y'` (amarillo), `'k'` (negro), `'w'` (blanco).
		- **Estilo de línea**: `'-'` (línea sólida), `'--'` (línea discontinua), `'-.'` (línea punteada), `':'` (línea de puntos).
		- **Marcador**: `'.'` (punto), `'o'` (círculo), `'x'` (x), `'+'` (cruz), `'*'` (asterisco), `'s'` (cuadrado), etc.
	- **Ejemplos**
		- `'ro'`: Puntos rojos (color `'r'` y marcador `'o'`).
		- `'g--'`: Línea verde discontinua (color `'g'` y estilo de línea `'--'`).
		- `'b-.'`: Línea azul punteada (color `'b'` y estilo de línea `'-.'`).
