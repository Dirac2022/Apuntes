
# Filtro espacial de imágenes



## Aplicaciones de filtros de imágenes

- Mejora de imágenes
- Remover ruido
- Detección de bordes
- Template matching

## Filtro

- Es un "prestamo" del procesamiento en el dominio de la frecuencia.
	- Vamos a distinguir: dominio espacial y dominio de la frecuencia.
- Filtros que dejan pasar información de baja frecuencia se conocen como **low-pass** filters.
- Filtros que dejan pasar información de alta frecuencia se conocen como **high-pass** filters.




![1hOI0jW3CcS_yuxcmJIYjKw.gif (495×576)](https://towardsdatascience.com/wp-content/uploads/2019/11/1hOI0jW3CcS_yuxcmJIYjKw.gif)



## Filtro

# Correlación vs Convolución
La operación convolucional ampliamente utilizada en CNN es un nombre inapropiado. La operación que se utiliza es, estrictamente hablando, una correlación en lugar de una convolución. Ambos operadores tienen una ligera diferencia.

## Correlación cruzada
La correlación es el proceso de mover una máscara de filtro, a menudo denominada kernel, sobre la imagen y calcular la suma de los productos en cada ubicación. La correlación es la función de desplazamiento del filtro.

![1WncBBUvi7lpWl-T1d2SlfQ-1024x358.png (1024×358)](https://towardsdatascience.com/wp-content/uploads/2019/11/1WncBBUvi7lpWl-T1d2SlfQ-1024x358.png)
![1EnH-qswA8Ip8YqrwDLCROw-1024x328.png (1024×328)](https://towardsdatascience.com/wp-content/uploads/2019/11/1EnH-qswA8Ip8YqrwDLCROw-1024x328.png)


Convenientemente supongamos que $F$ tiene un número impar de elementos, por lo que podemos suponer que a medida que se desplaza, su centro está junto encima de un elemento de la imagen $I$. Entonces decimos que $F$ tiene $2N+1$ elementos, y estos están indexados de $-N$ a $N$, de modo que el elemento central de $F$ es $F(0)$.


$$
F \ \circ \ I \ (x) = \sum_{i=-N}^N F(i) \ I(x+i)
$$
Extendiendo la operación a 2-D. Suponiendo que nuestro filtro tiene un número impar de elementos.

$$
F \ \circ \ I \ (x, y) = \sum_{j=-N}^N \sum_{i=-N}^N F(i, j) \ I(x+i, y+j)
$$

La operación de correlación en 2D tiene dos propiedades
1. **Invarianza traslacional**: Nuestro sistema de visión debe ser el de sentir, responder o detectar el mismo objeto independientemente de dónde aparezca en la imagen.
2. **Localidad**: Nuestro sistema de visión se centra en las regiones locales, sin tener en cuenta lo que está sucediendo en otras partes de la imagen.


```python
def cross_correlation1D(F, I, x):
  """  
  Computes the cross-correlation between a filter F and a signal I at a given position x.

  Parameters:
  -----------
  F : numpy array
    The filter.
  I : numpy array
    The signal.
  x : int
    The position at which to compute the cross-correlation.

  Returns:
  --------
  sum : float
    The cross-correlation between F and I at position x
  """
  N = len(F)
  offset = N - x
  sum = 0
  for i in range(N):
    product =  F[i] * I[offset + i]
    print(f'F({i}) * I({offset + i}) = {product}')
    sum += product
  print(f'F o I({x}) = {sum}')
  return sum
```


## Convolución
En la operación de convolución el kernel primero se voltea en un ángulo de 180° grados (se invierte) y luego se aplica a la imagen. 

$$
F \ * I \ (x) = \sum_{i=-N}^N F(i) \ I(x-i) 
$$
En el caso de convolución 2D, volteamos el filtro tanto horizontal como verticalmente.

$$
F \ ** \ I \ (x, y) = \sum_{j=-N}^N \sum_{i=-N}^N F(i, j) \ I(x-i, y-j)
$$

Las mismas propiedades de **invariancia traslacional** y **localidad** también son seguidas por la operación de convolución.


# Detección de bordes

![Figure_1-3.png (844×275)](https://hinumduman.home.blog/wp-content/uploads/2018/12/Figure_1-3.png)

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
Este calor indica la intensidad del borde en ese punto de la imagen.



### Pasos para aplicar el Filtro Sobel en una imagen (512x512)

1. **Tener la imagen en escala de grises**
2. **Definir los kernels Sobel**
3. **Crear una matriz vacía para almacenar el resultado**
	- Se necesita una matriz nueva de 512x512 para almacenar la imagen procesada.
4. **Recorrer la imagen aplicando el filtro Sobel**
    - Como los kernels tienen un tamaño de **3x3**, necesitas recorrer **cada píxel** desde **(1,1) hasta (510,510)** (excluyendo los bordes).
    - Para cada píxel **(i, j)**:
        1. **Extraer una ventana de 3×3** centrada en **(i, j)**.
        2. **Multiplicar esta ventana** con $G_x$ y $G_y$ (elemento por elemento).
        3. **Sumar los resultados** para obtener $S_x$ y $S_y$.
        4. **Calcular la magnitud del gradiente**:
            $$G = \sqrt{S_x^2 + S_y^2}$$
        5. **Asignar $G$ a la nueva imagen**.
5. **Normalizar los valores**
    - La imagen resultante puede tener valores fuera del rango **0-255**, así que debes normalizar los valores para que queden dentro de este rango.
6. **Retornar la imagen con los bordes detectados**
    - Una vez aplicado Sobel, puedes devolver la nueva imagen.



```python
def detection_border_sobel(image):
  """
  Applies the Sobel edge detection filter to grayscale image.

  Parameters:
  -----------
  image: numpy.ndarray
    A 2D NumPy array representing a grayscale image with pixel values in [0, 255].

  Returns:
  --------
  im_border: numpy.ndarray
    A 2D NumPy array representing the image with detected edges.
  """
  # Sobel kernels for detecting horizontal and vertical edges
  G_y = np.array([[-1, -2, -1],
                    [ 0,  0,  0],
                    [ 1,  2,  1]])
  G_x = np.array([[-1, 0, 1],
                    [-2, 0, 2],
                    [-1, 0, 1]])
  
  # Dimensions of the input image
  M, N = image.shape

  # Initialize an empty matrix to store edge magnitudes
  im_border = np.zeros((M, N))

  # Iterate over the image, avoiding the edges
  for i in range(1, M-1):
    for j in range(1, N-1):
      sub_image = image[i-1 : i+2 , j-1 : j+2]
      S_x = np.sum(G_x * sub_image)
      S_y = np.sum(G_y * sub_image)
      G = np.sqrt(S_x**2 + S_y**2)
      im_border[i, j] = G 

  # filter_X = cv2.filter2D(image, -1, G_x)
  # filter_Y = cv2.filter2D(image, -1, G_y)
  im_border = np.sqrt(filter_X**2 + filter_Y**2)

  # Normalize the image to scale values between 0 and 255
  max = np.max(im_border)
  min = np.min(im_border)
  im_border = 255 * (im_border - min) / (max - min)

  return im_border
```


## Operador Prewitt
El **operador de Prewitt** es un filtro que calcula las derivadas parciales de la imagen en las direcciones $X$ e $Y$, similar al operador [[Semana 3#Operador Sobel|Sobel]]. Se utiliza para detectar bordes en imágenes al resaltar las variaciones de intensidad en ambas direcciones.

>[!important] La diferencia principal con Sobel es que Prewitt utiliza un peso uniforme en los coeficientes del kernel, lo que lo hace más simple pero menos preciso frente al ruido.

$$
G_x = 
\begin{bmatrix}
-1 & 0 & 1 \\
-1 & 0 & 1 \\
-1 & 0 & 1 \\
\end{bmatrix}
$$

$$
G_y = 
\begin{bmatrix}
-1 & -1 & -1 \\
0 & 0 & 0 \\
1 & 1 & 1
\end{bmatrix}
$$

Al aplicar estos filtros a la imagen, se resaltan los cambios de intensidad en las direcciones horizontal y vertical. 
La **magnitud del gradiente** se puede calcular como:
$$
\text{Magnitud} = \sqrt{G_x^2 + G_y^2}
$$

| Característica                       | Sobel                                 | Prewitt                  |
| ------------------------------------ | ------------------------------------- | ------------------------ |
| **Pesos en el kernel**               | Mayor peso en la fila/columna central | Pesos uniformes          |
| **Sensibilidad al ruido**            | Más resistente al ruido               | Más sensible al ruido    |
| **Precisión en detección de bordes** | Más precisa                           | Menos precisa            |
| **Cálculo computacional**            | Un poco más costoso                   | Más simple y rápido      |
| **Uso recomendado**                  | Imágenes con ruido                    | Imágenes sin mucho ruido |

# Laplaciano de una Gaussiana

El **Laplaciano de una Gaussiana (LoG)** es un operador utilizado en procesamiento de imágenes para detectar bordes. Este método combina dos operaciones:

1. **Suavizando con una función Gaussiana** para reducir el ruido
2. **Aplicación del operador Laplaciano** para detectar regiones de cambio brusco en la intensidad de la imagen (bordes).

**Suavizando con la Gaussiana**

$$
G(x, y) = \dfrac{1}{2\pi \sigma^2} \ e^{-\frac{x^2 + y^2}{2\sigma^2}}
$$
- Un $\sigma$ grande difumina más la imagen, eliminando detalles finos.
- Un $\sigma$ conserva más detalles, pero puede dejar más ruido.

**Aplicación del Laplaciano**
El operador Laplaciano es un filtro de segunda derivada que detecta variaciones en la intensidad de la imagen. Se define como

$$
\nabla^2 I = \dfrac{\partial^2 I}{\partial x^2} + \dfrac{\partial^2 I}{\partial y^2}
$$
El Laplaciano realza las áreas donde la intensidad cambia abruptamente, lo que hace efectivo para detectar bordes.


El kernel de **LoG** se construye aplicando el operador Laplaciano a la función Gaussiana, dando lugar a una máscara como esta para un tamaño 5x5

$$
\begin{bmatrix} 
0 & 0 & -1 & 0 & 0 \\ 
0 & -1 & -2 & -1 & 0 \\ 
-1 & -2 & 16 & -2 & -1 \\ 
0 & -1 & -2 & -1 & 0 \\ 
0 & 0 & -1 & 0 & 0 
\end{bmatrix}
$$

# Filtro de la mediana

Se utiliza para reducir el ruido mientras se preservan los bordes. Es especialmente eficaz contra el **ruido impulsivo** o **sal y pimienta** (pixeles aleatorios blancos y negros).

1. Primero se define un tamaño de ventana (kernel), de 3x3, 5x5, etc.
2. Para cada pixel en la imagen se remplaza por la mediana de la vecindad de los pixeles.

![551px-Median_filter_2D.gif (551×599)](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Median_filter_2D.gif/551px-Median_filter_2D.gif)


```python
def median_filter(im, k=5):
  """
  Applies a median filter to a grayscale image

  Parameters:
  -----------
  im: numpy.ndarray
    A 2D NumPy array representing a grayscale image with pixel values in [0, 255].
  k: int
    The size of the filter (msut be an odd numeber).

  Returns:
  numpy.ndarray
    Filtered image with the median applied.
  """
  m, n = im.shape
  im_median = np.zeros((m, n))

  # Define the offset for the kernel (half the kernel size)
  offset = k // 2

  for i in range(offset, m-offset):
    for j in range(offset, n-offset):
      # Extract the kxk window centered at (i, j), compute the median of the window
      # and assign it to the corresponding pixel
      im_median[i, j] = np.median(im[i-offset: i+offset, j-offset: j+offset])
  return im_median
```
