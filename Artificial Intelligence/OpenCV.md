
# `GaussianBlur`
Aplica un filtro de desenfoque a las imágenes utilizando una distribución gaussiana. Este filtro suaviza la imagen y es efectivo para reducir el ruido y los detalles finos antes del procesamiento de imágenes.

## Filtro gaussiano
El filtro gaussiano se basa en la **función gaussiana**, que es una distribución de probabilidad en forma de campana, y se utiliza para calcular una ponderación para los píxeles en la vecindad de un píxel central. Esta ponderación hace que los píxeles más cercanos al centro del filtro tengan mayor influencia en el valor calculado para el píxel resultante.

La forma matemática de la distribución gaussiana es la siguiente:
$$
f(x, y) = \frac{1}{2 \pi \sigma^2} \exp \left( -\frac{x^2 + y^2}{2 \sigma^2} \right)
$$

Donde:

- $f(x,y)$ es el valor de la función en las coordenadas $(x,y)$.
- $\sigma$ es la desviación estándar de la distribución gaussiana, que determina el "ancho" de la campana. (cómo de difusa o concentrada es la campana).
- $x$ y $y$ son las distancias relativas desde el centro del filtro.

## Sintaxis
```python
cv2.GaussianBlur(src, ksize, sigmaX[, sigmaY[, borderType]])
```

1. **`src`**: La imagen de entrada sobre la que se va a aplicar el filtro. Debe ser una matriz de píxeles (por ejemplo, una imagen cargada con `cv2.imread`).
    
2. **`ksize`**: El tamaño del **kernel** (o máscara) gaussiana. Es un valor de la forma `(ancho, alto)`, donde tanto el ancho como el alto deben ser números impares (por ejemplo, `(3, 3)`, `(5, 5)`, `(7, 7)`). Un tamaño de kernel mayor tiene un mayor efecto de desenfoque.
    - El kernel define el área de los píxeles que se usan para calcular el nuevo valor de un píxel en la imagen.
    - Típicamente, se usan valores impares porque el centro del kernel debe ser un píxel específico.
3. **`sigmaX`**: La desviación estándar en la dirección **X** (horizontal). Controla la "cantidad" de suavizado que se aplica en esa dirección. Si se establece en 0, OpenCV calcula automáticamente un valor adecuado de `sigmaX` en función del tamaño del kernel.
    
4. **`sigmaY`**: La desviación estándar en la dirección **Y** (vertical). Si se omite, se asume que es igual a `sigmaX`. Si se establece en 0, se calcula automáticamente, al igual que para `sigmaX`.
    
5. **`borderType`** (opcional): Define cómo manejar los bordes de la imagen cuando el filtro no puede ser completamente aplicado debido a la proximidad de los bordes de la imagen. Por defecto, este parámetro es `cv2.BORDER_DEFAULT`. Otros valores incluyen:
    - `cv2.BORDER_CONSTANT`: Rellenar con un valor constante (por defecto 0).
    - `cv2.BORDER_REFLECT`: Reflejar los píxeles en los bordes.
    - `cv2.BORDER_REPLICATE`: Replicar los píxeles del borde.


# `cv2.Sobel`
Se usa para aplicar el **Operador de Sobel**, un filtro común en procesamiento de imágenes para detectar bordes. Este operador utiliza derivadas espaciales para calcular el cambio de intensidad en la imagen, permitiendo resaltar los bordes de los objetos.

## Operador Sobel
El **operador de Sobel** es un filtro que calcula las derivadas parciales de la imagen en las direcciones $X$ (horizontal) e $Y$ (vertical). Estas derivadas se combinan para obtener la magnitud del borde en cada píxel de la imagen.

Los filtros de Sobel son máscaras o kernels que se aplican a la imagen para aproximar las derivadas de primer orden. En otras palabras, el operador calcula el cambio de la intensidad de la imagen en ambas direcciones (horizontal y vertical), lo que permite detectar los bordes.

### Fórmulas de los kernels de Sobel

Los kernels de Sobel para las direcciones $X$ y $Y$ son:

**Kernel en la dirección $X$**
$$
G_x = \begin{bmatrix}
1 & 0 & -1 \\
2 & 0 & -2 \\
1 & 0 & -1
\end{bmatrix}
$$
**Kernel en la dirección $Y$**

$$
G_y = \begin{bmatrix}
1 & 2 & 1 \\
0 & 0 & 0 \\
-1 & -2 & -1
\end{bmatrix}
$$

Al aplicar estos filtros a la imagen, se resalta el cambio de intensidad en las direcciones horizontal y vertical. La **magnitud del gradiente** se puede calcular usando la siguiente formula
$$
\text{Magnitud} = \sqrt{G_x^2 + G_y^2}
$$
Este calor indica la intensidad del borde en ese punto de la imagen

## Sintaxis

La función `cv2.Sobel` tiene la siguiente forma:
```python
`cv2.Sobel(src, ddepth, dx, dy, ksize, scale=1, delta=0, borderType=cv2.BORDER_DEFAULT)`
```


1. **`src`**: La imagen de entrada (en formato de matriz de píxeles), que generalmente debe estar en escala de grises para que el filtro Sobel funcione de manera óptima.
2. **`ddepth`**: La profundidad de la imagen de salida (tipo de datos del resultado).
    - Se puede usar `-1` para mantener la misma profundidad que la imagen de entrada.
    - Ejemplo: `cv2.CV_8U`, `cv2.CV_64F`.
3. **`dx`**: El orden de la derivada en la dirección **X**.
    - Para detectar bordes horizontales, se pone `dx = 1` y `dy = 0`.
    - Para detectar bordes verticales, se pone `dx = 0` y `dy = 1`.
4. **`dy`**: El orden de la derivada en la dirección **Y**.
5. **`ksize`**: El tamaño del kernel de Sobel. Un valor común es 3 (el tamaño de la máscara de 3x3). Puede ser 1, 3, 5, 7, etc. (siendo 3 el valor más común).
6. **`scale`** (opcional): Un factor de escala que puede ajustarse para cambiar la magnitud de la salida. Por defecto es 1.
7. **`delta`** (opcional): Un valor adicional que se suma al resultado. El valor por defecto es 0.
8. **`borderType`** (opcional): El tipo de borde a utilizar para los bordes de la imagen cuando el filtro no puede ser completamente aplicado (por ejemplo, en los bordes de la imagen). El valor por defecto es `cv2.BORDER_DEFAULT`.
