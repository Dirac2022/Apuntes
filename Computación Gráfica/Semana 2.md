
# Mezcla de colores

Colores primarios y secundarios de luz y pigmentos.

![dac1_1.png (602×251)](https://discountartncraftwarehouse.com.au/dac/assets/media/dac1_1.png)

# Características de colores

- **Brillo** : Noción acromática de la intensidad.
	- Se refiere a la intensidad de la luz, sin considerar el color.
	- Un mismo color puede verde más brillante o más oscuro dependiendo de la cantidad de luz.
- **Matiz (Hue)** : El atributo relacionado con la longitud de onda.
	- Es lo que comúnmente llamamos "color" (rojo, verde, azul, etc.)
- **Saturación** : Se refiere a la pureza relativa o la cantidad de luz blanca mezclada con el matiz.
	- Un color saturado es muy vivo, mientras que uno menos saturado se mezcla con blanco y parece más apagado o grisáceo.

> [!note] Cromaticidad
> La cromaticidad es la combinación de **matiz** y **saturación**. Es decir, describe el color sin importar su brillo.


# Modelo de Trí-Estimulo
El modelo de trí-estímulo se basa en cómo el ojo humano percibe el color a través de tres receptores (conos sensibles a Rojo, Verde y Azul).

Los valores $X, Y, Z$ corresponden al modelo $\textbf{CIE 1931 XYZ}$ que es un estándar en colorimetría.

Se define un sistema de **coordenadas normalizadas** para describir el color de manera independiente de la intensidad

$$
x= \dfrac{X}{X+Y+Z}
$$

$$
y = \dfrac{Y}{X+Y+Z}
$$

$$
z = \dfrac{Z}{X+Y+Z}
$$

Siempre se cumple que
$$
x + y + z = 1
$$

Por lo tanto, solo se necesitan dos valores $(x, y$ para representar la cromaticidad, ya que el tercero se deduce.

# Gamut
Es el rango que puede ser representado por un dispositivo. (ej. pantalla o impresora).

Cada pantalla, impresora o cámara tiene un rango limitado de colores que puede mostrar o capturar. Este rango depende de las características físicas del dispositivo y del espacio de color que utilice (RGB, CMYK, etc).


# RGB
RGB (Red, Green, Blue) es un modelo de color basado en la **mezcla aditiva** de luz. Se usa en pantallas y dispositivos digitales. Cada color se representa con tres valores en un rango de 0 a 255.


<img src="https://www.researchgate.net/profile/Dr-Kashmar/publication/335504961/figure/fig1/AS:797662513217546@1567188971536/Figure-11-The-Normalization-of-RGB-color-values80_W640.jpg" width=600>


# CMYK
CMYK(Cyan, Magenta, Yellow, Black) es un modelo basado en la **mezcla sustractiva** de tintas. Se usa en impresión. Cada color se representa con cuatro valores en un rango de 0 a 1.


# CMY
El modelo CMY(Cyan, Magenta, Yellow) es un modelo de color sustractivo que se basa en la absorción de luz. Es una versión simplificada de CMYK, pero sin el componente negro (K).

$$
\begin{bmatrix}
C \\
M \\
Y
\end{bmatrix}
=
\begin{bmatrix}
1\\
1 \\
1
\end{bmatrix}
-
\begin{bmatrix}
R \\
G \\
B
\end{bmatrix}
$$

>[!info] Este modelo se usa en impresión y tintas porque los colores se generan reflejando y absorbiendo luz en vez de emitirla.


# HSI
Los modelos de color como RGB y CMY(K) son útiles para dispositivos electrónicos e impresión, pero no representan el color como lo percibe el ojo humano.

El modelo HSI (Hue, Saturation, Intensity) se basa en cómo los humanos perciben el color y es ideal para procesamiento de imágenes, visión artificial y análisis de color.

HSI divide el color en tres componentes independientes:

1. Matiz (Hue, H) : El color puro que vemos.
2. Saturación: La intensidad o pureza del color.
3. Intensidad: El brillo o nivel de luz en la imágen.

## Matiz
Representa el color base en un círculo de 360°
- $0°$ = Rojo
- $120°$ = Verde
- $240°$ = Azul

Se calcula como
$$
H = cos^{-1} \left(\dfrac{(R-G) + (R-B)}{2 \sqrt{(R-G)^2 + (R-B)(G-B)}} \right)
$$

Si $B > G$, entonces $H = 360° - H$

## Saturación
Mide cuán puro o desaturado es un color. Un color $100 \%$ saturado es puro, mientras que $0 \%$ saturado es un tono de gris.

$$
S = 1 - \frac{\text{min}(R, G, B)}{I}
$$
**Ejemplo**
- Un rojo puro (255, 0, 0) tiene S=1 (máxima saturación)
- Un rosa (255, 150, 150) tiene S<1 porque está más desaturado

## Intensidad
Es e brillo promedio del color, definido como
$$
I = \frac{R+G+B}{3}
$$

# HSV
El modelo HSV (Hue, Saturation, Value) es una variante del HSI que también se basa en la percepción humana del color, pero con una diferencia en cómo representa el brillo

1. Matiz : Igual que en HSI
2. Saturación : Igual que en HSI
3. Valor (Value) : Representa el brillo del color
	- 0 = Negro (sin luz), 100% = Máximo brillo.

>[!tip] En HSI, la intensidad (I) es el promedio de R, G y B. Mientras que en HSV, V es simplemente el máximo de R, G y B


## **2. Conversión entre RGB y HSV**

Para convertir de **RGB a HSV**, seguimos estos pasos:

1. Calcular el Matiz (H, en grados):  
    $$H = \cos^{-1} \left( \frac{(R - G) + (R - B)}{2 \sqrt{(R - G)^2 + (R - B)(G - B)}} \right)$$
    
    - Si B > G, entonces H = 360° - H.
    
2. Calcular la Saturación (S, en porcentaje):  
    $$S = \frac{V - \min(R, G, B)}{V}$$​
    - Donde V = max(R, G, B)
    
3. Calcular el Valor (V, brillo máximo):  
    $$V = \max(R, G, B)$$
    

**Conversión inversa (HSV → RGB)** se hace por segmentos, dependiendo de en qué rango esté el matiz **H**.