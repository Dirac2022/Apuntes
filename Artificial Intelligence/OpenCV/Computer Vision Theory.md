[Computer Vision codes.ipynb - Colab](https://colab.research.google.com/drive/1a0Bqacodk5o8Byx_6gLrC1bUt5WCFgGW#scrollTo=ISKDBxjfLQtf)


# Filtro gaussiano
El filtro gaussiano se basa en la **función gaussiana**, que es una distribución de probabilidad en forma de campana, y se utiliza para calcular una ponderación para los píxeles en la vecindad de un píxel central. Esta ponderación hace que los píxeles más cercanos al centro del filtro tengan mayor influencia en el valor calculado para el píxel resultante.

La forma matemática de la distribución gaussiana es la siguiente:
$$
f(x, y) = \frac{1}{2 \pi \sigma^2} \exp \left( -\frac{x^2 + y^2}{2 \sigma^2} \right)
$$

Donde:

- $f(x,y)$ es el valor de la función en las coordenadas $(x,y)$.
- $\sigma$ es la desviación estándar de la distribución gaussiana, que determina el "ancho" de la campana. (cómo de difusa o concentrada es la campana).
- $x$ y $y$ son las distancias relativas desde el centro del filtro.


# Canny Edge Detection
Is a popular edge detection algorithm. It is a multi-stage algorithm:

1. **Noise Reduction**
2. **Finding Intensity Gradient of the Image**
3. **Applying Non-Maximum Suppression**
4. **Hysteresis Thresholding**


## Noise Reduction
Since edge detection is susceptible to noise in the image, first step is to remove the noise in the image with a 5x5 Gaussian filter.

## Finding Intensity Gradient of the Image
Smoothened image is then filtered with a Sobel kernel in both horizontal and vertical direction to get fist derivative in horizontal direction ($G_x$) and vertical direction ($G_y$). From these two images, we can find edge gradient and direction for each pixel as follows


$$
\text{Gradient Magnitude} \, (G) = \sqrt{G_x^2 + G_y^2}
$$

$$
\text{Gradient direction} \, (\theta) = \tan^{-1} \left( \frac{G_y}{G_x} \right)
$$
Gradient direction is always perpendicular to edges. It is rounded to one of four angles representing vertical, horizontal and two diagonal directions.

## Non-maximum Suppression
After getting gradient magnitude and direction, a full scan of image is done to remove any unwanted pixels which may not constitute the edge. For this, at every pixel is checked if it a local maximum in its neighborhood in the direction of gradient.

![nms.jpg (450×198)](https://docs.opencv.org/4.x/nms.jpg)

Point A is on the edge (in vertical direction). Gradient direction is normal to the edge. Point B and C are in gradient directions. So point A is checked with point B and C to see if it forms a local maximum. If so, it is considered for next stage, otherwise, it is suppressed (put to zero).

---
>[!tip] **Non-maximum Suppression** aims to thing out detected edges by removing pixels that do not represent a true edge

After computing gradients using **Sobel filters**, we obtain an image with many intensity variations, but not all these represent real edges. **NMS helps reduce edge thickness**.

### Steps
**NMS** operates on the gradient magnitude image and follows these steps
#### 1. Input
- A matrix containing the **gradient magnitude** $G$, computed as:  
    $G = \sqrt{G_x^2 + G_y^2}​​$
- A matrix containing the **gradient direction** $θ$:  
    $\theta = \tan^{-1} \left(\frac{G_y}{G_x} \right)$

- The magnitude indicates how strong the edge is at each pixel.  
- The direction indicates where the intensity change is pointing.

---

#### 2. Assigning Edge Directions to 4 categories

The values of $\theta$ can be any angle between $0°$ and $360°$, but for simplicity, they are rounded to one of 4 main directions based on proximity.

| Direction                    | $θ$ interval                 | Approximate Edge Orientation |
| ---------------------------- | ---------------------------- | ---------------------------- |
| **0° (horizontal)**          | 0° a 22.5° or 157.5° to 180° | Left ↔ Right                 |
| **45° (diagonal positive)**  | 22.5° to 67.5°               | Bottom-left ↙ Top-right ↗    |
| **90° (vertical)**           | 67.5° to 112.5°              | Top ↑ Bottom ↓               |
| **135° (diagonal negative)** | 112.5° to 157.5°             | Bottom-right ↘ Top-Left ↖    |

#### 3. Comparing with Neighboring Pixels

For each pixel in the image:

- Its edge direction is determined.
- Two neighboring pixels in the gradient direction are compared.
- If the current pixel is smaller than either neighbor, it is suppressed (set to 0).

Example in 4 possible directions:

1. If the edge is horizontal (0°): Compare with **left and right** pixels.
2. If the edge is diagonal positive (45°): Compare with **diagonal** pixels in that direction.
3. If the edge is vertical (90°): Compare with **top and bottom** pixels.
4. If the edge is diagonal negative (135°): Compare with **diagonal** pixels in that direction.

If a pixel is not a local maximum, it is removed (set to 0 in the image).

#### 4. Producing the Final Thinned Edges

After applying this suppression, the edges become **much thinner** and more precisely.


#### Visual example
Let's say we have an edge-detected image with the following gradient magnitude values:

```
  0   0  50  100  50   0   0
  0  30  80  150  80  30   0
  0  10  40   80  40  10   0
```

If the **gradient** indicates that the edges are in the **horizontal direction**, we compare each pixel with its left and right neighbors..

Before NMS (thick edges):

```
  0   0  50 100  50   0   0
  0  30  80 150  80  30   0
  0  10  40  80  40  10   0
```

After NMS (thinned edges):

```
  0   0   0 100   0   0   0
  0   0   0 150   0   0   0
  0   0   0  80   0   0   0
```

Only the pixel with the maximum intensity in each edge direction is retained.


# Image rotation

When rotating an image, each pixel $(x, y)$ is mapped to a new position $(x', y')$ based on the rotation matrix

$$
\begin{bmatrix}
 x' \\
 y'
\end{bmatrix} 
=
\begin{bmatrix}
 cos(\theta) & - sin(\theta) & tx \\
 sin(\theta) & cos(\theta) & ty
\end{bmatrix} 
\begin{bmatrix}
 x \\
 y
\end{bmatrix} 
$$

Where
- $\theta$ is the rotation angle in radians
- `(tx, ty)` is the translation required to keep the center fixed