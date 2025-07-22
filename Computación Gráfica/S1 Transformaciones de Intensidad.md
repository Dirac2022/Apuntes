

Las transformaciones de intensidad son operaciones que modifican los valores de los píxeles en una imagen, con el objetivo de mejorar el contraste, resaltar detalles o realizar análisis de la imagen. Estas transformaciones pueden ser lineales o no lineales y se aplican a cada píxel de manera independiente.

Matemáticamente, una transformación de intensidad se expresa como:

$g(x,y) = T[f(x,y)]$

donde:

- $f(x,y)$ es la intensidad del píxel en la imagen original.
- $g(x,y)$ es la intensidad transformada del píxel.
- $T$ es la función de transformación aplicada a cada píxel.


# Escala de Intensidad

La escala de intensidad se refiere al rango de valores que pueden tomar los píxeles de una imagen.

- **Imágenes en escala de grises**: Cada píxel tiene un valor de intensidad entre 0 (negro) y 255 (blanco) en imágenes de 8 bits.
- **Imágenes en color**: Se representan con modelos como RGB, donde cada canal (rojo, verde, azul) tiene intensidades de 0 a 255.

Ejemplo de una imagen en escala de grises:

$$
\begin{bmatrix} 
120 & 130 & 140 \\ 
150 & 160 & 170 \\ 
180 & 190 & 200 
\end{bmatrix}
$$

# Transformación de Intensidad: Negativo de una Imagen


![bw-negative.jpg (1000×665)](https://www.guidetofilmphotography.com/photos/bw-negative.jpg)

El negativo de una imagen invierte los valores de intensidad, transformando áreas claras en oscuras y viceversa.

La fórmula para obtener el negativo es:  
$g(x,y) = L - 1 - f(x,y)$
donde:

- $L$ es el número total de niveles de intensidad (256 en imágenes de 8 bits).
- $f(x,y)$ es la intensidad original del píxel.

Ejemplo de transformación:

$$
f(x,y) = 
\begin{bmatrix} 
120 & 130 & 140 
\\ 150 & 160 & 170 
\\ 180 & 190 & 200 
\end{bmatrix}
$$

Aplicando $g(x,y) = 255 - f(x,y)$:

$$
g(x,y) = 
\begin{bmatrix} 
135 & 125 & 115 \\ 
105 & 95 & 85 \\ 
75 & 65 & 55 
\end{bmatrix}
$$

Esto genera un efecto de imagen en negativo.

## Aplicaciones del Negativo de una Imagen

- **Realce de detalles en imágenes médicas**: Se usa para mejorar la visibilidad de estructuras en radiografías.
- **Procesamiento de imágenes astronómicas**: Resalta detalles en imágenes captadas por telescopios.


# Revelar una Imagen en Negativo

Revelar una imagen en negativo implica visualizar la imagen negativa antes de transformarla nuevamente a positiva.

## Proceso de revelado digital

1. Captura o carga de la imagen original.
2. Aplicación de la transformación de negativo.
3. Visualización de la imagen transformada.

En términos de software, esto se implementa en Python con OpenCV:

```python
import cv2
import numpy as np

# Cargar imagen en escala de grises
imagen = cv2.imread("imagen.jpg", cv2.IMREAD_GRAYSCALE)

# Aplicar transformación negativa
negativo = 255 - imagen

# Mostrar imagen original y negativa
cv2.imshow("Original", imagen)
cv2.imshow("Negativo", negativo)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## Transformación de Intensidad: Negativo -> Positivo

Para convertir un negativo en una imagen positiva, se aplica nuevamente la ecuación:

$g(x,y) = 255 - f(x,y)$

Si partimos de una imagen negativa, al aplicar esta operación obtenemos la imagen original.

Ejemplo práctico en Python:

```python
# Convertir imagen negativa a positiva
positivo = 255 - negativo

cv2.imshow("Positivo", positivo)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

**Aplicaciones**

- Restauración de imágenes en negativo en fotografía analógica.
- Digitalización de documentos antiguos.


## Transformación de Intensidad: Positivo -> Negativo

El proceso inverso también se usa en imágenes fotográficas y en procesamiento de imágenes médicas.

```python
negativo_nuevo = 255 - imagen
```

Esto permite resaltar contornos y contrastes en imágenes con bajo nivel de detalle.


# Thresholding

La umbralización (Thresholding) es una técnica para segmentar una imagen, convirtiéndola en binaria (blanco y negro).

### Fórmula

$$
\begin{cases} 
0, & \text{si } f(x,y) < T \\ 
255, & \text{si } f(x,y) \geq T 
\end{cases}
$$

donde $T$ es un umbral definido por el usuario.

Ejemplo de umbralización con umbral $T = 150$:

$$
\begin{bmatrix} 
120 & 130 & 140 \\ 
150 & 160 & 170 \\ 
180 & 190 & 200 
\end{bmatrix}
$$

$$
\text{Umbralizada} = 
\begin{bmatrix} 0 & 0 & 0 \\ 
255 & 255 & 255 \\ 
255 & 255 & 255 
\end{bmatrix}
$$


## Types of Thresholding

| Type                  | Description                                                                                                                 |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Simple Thresholding   | A single threshold value is used to separate pixels into black or white                                                     |
| Adaptive Thresholding | The threshold value varies depending on the local region of the image, useful for images with uneven (iluminación) lighting |
| Otsu's Thresholding   | Automatically calculates an optimal threshold value using image histogram analysis                                          |

### Adaptive Thresholding
Is a technique used when an image has varying lighting conditions. Instead of using a single threshold value for the entire image, it calculates different threshold values for different regions of the image.

## Implementation

En OpenCV, se implementa así:

```python
_, umbralizada = cv2.threshold(imagen, 150, 255, cv2.THRESH_BINARY)

cv2.imshow("Umbralizada", umbralizada)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

**Aplicaciones de la Umbralización**

- Segmentación de texto en documentos escaneados.
- Detección de objetos en visión artificial.
- Reducción de ruido en imágenes médicas.

