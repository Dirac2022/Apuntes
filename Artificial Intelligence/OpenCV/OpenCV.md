

# Installing OpenCV

```bash
pip install opencv-contrib-python
```

Se usa para instalar OpenCV junto con los módulos adicionales (contrib) que no están incluidos en la versión estándar de OpenCV. Para instalar solo los módulos principales de OpenCV:
```bash
pip install opencv-python
```

```
pip install caer
```
Instala **Caer**, una biblioteca de visión por computadora optimizada para la simplicidad y la velocidad. (Para el curso de OpenCV - freeCodeCamp.org). [jasmcaus/caer: High-performance Vision library in Python. Scale your research, not boilerplate.](https://github.com/jasmcaus/caer)



# Basics

## General

### `cv2.destroyAllWindows()`
Closes all OpenCV windows that were created with [[#cv2.imshow()]]. Prevents windows from staying open after the program ends.
```python
cv2.destroyAllWindows()
```
## Reading an image

### `cv2.imread()`
This method takes in a path to an image and returns that image as a matrix of pixels (NumPy array)

```python
img = cv2.imread('path-image', flag)
```

- `flag` (optional) : Defines how the images is loaded
	- `cv2.IMREAD_COLOR` (1): Loads the image in color (BGR format by default). Transparency is ignored
	- `cv2.IMREAD_GRAYSCALE` (0): Loads the image in grayscale.
	- `cv2.IMREAD_UNCHANGED` (-1): Loads the image with all channels, including the alpha channel (if available).

### `cv2.imshow()`
Is used to display an imagen in a window.
```python
cv2.imshow(window_name, image)
```

- `window_name` : Name of the window (string)
- `image` : Image to be displayed

### `cv2.waitKey()`
Is used to wait for a key press and handle window events.

```python
cv2.waitKey(delay)
```
- `delay` : Time in milliseconds to wait for a key press. If `delay = 0`, it waits indefinitelt until a key is pressed.

## Reading a video

### `cv2.VideoCapture()`
Is used to capture video from a file or a camera. This method returns a `cv2.VideoCapture` object which is used to control and read frames from a video or camera. 
```python
cap = cv2.VideoCapture(source)
```

- `source` : The video source, which can be:
	- `0` or `1` , etc. : For live video from a webcam (0 = default camera)
	- File path to read a video from a file

The `cv2.VideoCapture` instance allows you to
- Read frames `cap.read()`
- Check if the source is open `cap.isOpened()`
- Release the camera `cap.release()`

#### Methods

##### `cap.read()`
Is used to read the next frame from a video or camera

```python
ret, frame = cap.read()
```

- `ret` : `True` is the frame was read successfully, `False` if there is an issue.
- `frame` : The image captured from the video or camera (NumPy array)


##### `cap.release()`
Release the video capture object. Frees up system resources
```python
cap = cv2.VideoCapture(0)
# .. (read and display frames)
cap.release()
```

>[!tip] If you don´t call `cap.release()`, the camera might stay locked and unavailable for other programs.


## Resizing and Rescaling

Rescaling video implies modifying its height and width. Generally, it´s always best practice to downscale or change the width and height of your video files to a smaller value than the original dimensiones.


### `cv2.resize()`
Is used to resize (scale) an image to a different size.
```python
resized_image = cv2.resize(src, dsize, fx=scale_x, fy=scale_y, interpolation=method)
```

- `src` : The input image (NumPy array)
- `dsize` : The desired size `(width, height)`. If `None`, use `fx` and `fy`.
- `fx`, `fy` : Scale factor along the $X$-axis (width), $Y$-axis (height).
- `interpolation` : Method to resize the image.

|**Interpolation Method**|**When to Use?**|**Quality**|**Speed**|
|---|---|---|---|
|`cv2.INTER_NEAREST` (Nearest Neighbor)|Fastest method, but may produce blocky images. Used when speed is critical, like real-time applications.|Low (pixelated)|⚡ Fastest|
|`cv2.INTER_LINEAR` (Bilinear Interpolation)|Default method. Good balance between speed and quality. Best for **downscaling** small images.|Medium|🔹 Fast|
|`cv2.INTER_CUBIC` (Bicubic Interpolation)|Produces smoother results than bilinear. Best for **upscaling** images while preserving details.|High|⏳ Slower|
|`cv2.INTER_LANCZOS4` (Lanczos Interpolation)|Highest-quality method. Best for **high-resolution upscaling** but computationally expensive.|Very High|🐢 Slowest|
|`cv2.INTER_AREA` (Pixel Area Relation)|Best for **downscaling** images as it averages pixel regions. Reduces noise and aliasing.|High (for shrinking)|🔸 Moderate|



```python
import cv2

img = cv2.imread('image.jpg')

# Resize to 200x300 pixels
resized = cv2.resize(img, (200, 300))

# Resizing by scale factor
resized = cv2.resize(img, None, fx=0.5, fy=0.5) # Scale down to 50 %

```

## Drawing Shapes

Before we start drawing in OpenCV, we need a canvas where we can create shapes, lines, or text. We create a blank image (a black background) with three channels (BGR) where we can add our drawings.

```python
import numpy as np
import cv2

blank = np.zeros((500, 500, 3), dtype='uint8')
cv2.imshow('Blank', blank)
```


### `cv2.rectangle()`
Draw a rectangle on an image
```python
cv2.rectangle(image, pt1, pt2, color, thickness)
```

- `image` : The image where the rectangle will be drawn
- `pt1`, `pt2` : The top-left/bottom-right corner of the rectangle ($x_1, y_1$) / ($x_2, y_2$)
- `color` : The color of the rectangle `(B, G, R)`
- `thickness` : Line thickness (in pixels). `-1` to fill the rectangle or `cv2.FILL`
 
### `cv2.circle()`
Draw a circle on an image
```python
cv2.circle(image, center, radius, color, thickness)
```

- `center` : The center of the circle `(x, y)`
- `radius` : The radius of the circle (in pixels)

### `cv2.line()`
Draw a straight line on an image
```python
cv2.line(image, pt1, pt2, color, thickness)
```

# `GaussianBlur`
Aplica un filtro de desenfoque a las imágenes utilizando una distribución gaussiana. Este filtro suaviza la imagen y es efectivo para reducir el ruido y los detalles finos antes del procesamiento de imágenes.


## Text on image

### `cv2.putText()`
Draw text on an image
```python
cv2.putText(image, text, org, font, fontScale, color, thickness)
```

- `text` : The text string to display
- `org` : The bottom-left corner of the text `(x, y)`
- `font` : The font type (e.g., `cv2.FONT_HERSHEY_SIMPLEX`)
- `fontScale` : The size of the text


## Essential functions

### Converting to grayscale
Using the [[#Advanced#`cv2.cvtColor()`]] 
```python
# Coverting to grayscale
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('Gray', gray)
```


### `cv2.GaussianBlur()`
Is used to apply a [[Computer Vision Theory#Filtro gaussiano|Gaussian blur]] to an image. This helps in reducing noise, smoothing the image, and improving edge detection.
```python
blur_image = cv2.Gaussian(iamge, ksize, sigmaX)
```

- `image` : The input image to blur
- `ksize` : The size of the kernel (odd number, e.g., `(5,5)`). 
- `sigmaX` : Standard deviation in the $X$ direction (controls the blur amount)
	- `1` : light blur
	- `3` : stronger blur
	- `0` : OpenCV automatically selects `sigmaX`

💡 **Note:** The larger the kernel, the more blurred the image will be.


### `cv2.Canny()`
Is used to detect edges in an image using the **[[Computer Vision Theory#Canny Edge Detection|Canny Edge Detection algorithm]]** .
```python
cv2.Canny(image, threshold1, threshold2)
```

- `threshold1` : Lower threshold for edge detection
- `threshold2` : Upper threshold for edge detection 

| Lower (threshold1)        | Upper (threshold2)          | Effect                                                                     |
| ------------------------- | --------------------------- | -------------------------------------------------------------------------- |
| **Low** (e.g., `50`)      | **High** (e.g., `150`)      | ✅ **Good balance**, detects strong edges and keeps weak ones if connected. |
| **Low** (e.g., `30`)      | **High** (e.g., `200`)      | 🔍 **More edges**, but may increase noise.                                 |
| **High** (e.g., `100`)    | **Very High** (e.g., `200`) | ✂ **Fewer edges**, only detects strong ones.                               |
| **Very Low** (e.g., `10`) | **Very High** (e.g., `250`) | ❌ **Too many edges**, lots of noise.                                       |

**🔹 Rule of Thumb:** `threshold2 ≈ 2 × threshold1` (but this varies by image).


### `cv2.dilate()`
Is used to **expand** bright (white) regions in an image. It is commonly used in **morphological operations** to make objects thicker, fill small holes, or connect broken edges in binary images.

```python
dilated = cv2.dilate(src, kernel, iterations=1)
```

- `src` : Input image
- `kernel` : Structuring element (define how dilation spreads)
- `iterations` (opcional) : Number of times dilation is applied

**Steps**
- The kernel moves over the image.
- If any pixel inside the kernel is white (255), the center pixel becomes white.
- This expands bright areas and connects nearby objets.


### `cv2.erode()`
Is used to **shrink** bright (white) regions in an image. It is a fundamental **morphological operation** used to remove noise, detach connected objects, and refine shapes.

```python
eroded = cv2.erode(src, kernek, iterations=1)
```

**Steps**
- The kernel moves over the image
- If all pixels inside the kernel are white (255), the center pixel remains white.
- If any pixel inside the kernel is black (0), the center pixel becomes black.
- This **shrinks bright areas** and removes small white noise.




## Image Transformation


- translation
- rotation
- resizing
- flipping
	- cropping

### `cv2.warpAffine()`
Is used to apply an **affine transformation** to an image. This means the image can be translated, rotated, scaled, sheared, or any combination of these transformations while preserving parallelism (i.e., straight lines remain straight).

```python
dst = cv2.warpAffine(src, M, dsize[, dst[, flags[, borderMode[, borderValue]]]])
```

- `src` : Input image (grayscale or color)
- `M` : 2x3 affine transformation matrix (computed using `cv2.getRotationMatrix2D`) or `cv2.getAffineTransform()`
- `dsize` : Output image size `(width, height)`
- `dst` (optional) : Output image (same type as input)
- `flags` (optional) : Interpolation method (e.g., `cv2.INTER_LINEAR`, `cv2.INTER_CUBIC`)
- `borderMode` : How to handle pixels outside the image (e.g., `cv2.BORDER_CONSTANT`, `cv2.BORDER_REPLICATE`)
- `borderValue` (optional): Border color for `cv2.BORDER_CONSTANT` (default is black)



### `cv2.getRotationMatrix2D()`
Generates a 2x3 affine transformation matrix used for rotating an image around a specific point. This matrix is then used in `cv2.warpAffine()` to apply the rotation.

```python
M = cv2.getRotationMatrix2D(center, angle, scale)
```

- `center` : The point `(x, y)` around which the images is rotated
- `angle` : The rotation angle in degrees (positive = counterclockwise, negative = clockwise)
- `scale` : The scaling factor (>1 enlarge, <1 shrink)

### `cv2.flip()`
Mirrors (flip) an image along a specified axis.

```python
flipped = cv2.flip(img, flipCode)
```

- `flipCode` : Define the flipping direction
	- 0 : Vertically (upside-down)
	- 1 : Horizontally (left-right mirror)
	- -1 : Flip both vertically and horizontally



## Contour detection

### `cv2.findContours()`
```python
contours, hierarchy = cv2.findContours(image, mode, method[, offset])
```

- `image` : Input binary image (must be threshold or edge-detected first).
- `mode` : Contour retrieval mode. Determines how contours are stored and related
	- `cv2.RET_EXTERNAL` : 0. Retrieves only the outermost contours (ignores inner contours)
	- `cv2.RETR_LIST` : 1. Retrieves all contours but without hierarchy
	- `CV2.RETR_CCOMP`: 2. Retrieves all contours and organizes them into 2 levels (outer contours and inner holes)
	- `cv2.RETR_TREE` : 3. Retrieves all contours and reconstructs the full hierarchy of nested contours.
- `method` : Contour approximation method. Define how contour points are stored. The item is the value:
	1. `cv2.CHAIN_APPROX_NONE` : Stores all contour points (detailed, high memory use)
	2. `cv2.CHAIN_APPROX_SIMPLE` : Removes redundant points (saves memory)
	3. `cv2.CHAIN_APPROX_TC89_L1` : Uses Teh-Chin chain approximation for simplification.
	4. `cv2.CHAIN_APPROX_TC89_KCOS`: Another Teh-Chin approximation method (less detailed).
- `offset` (optional) : Shift contours by a given `(x, y)` offset

**Returns**
- `contours` : A list of NumPy array, where each array contains `(x, y)` points forming a contour.
- `hierarchy` : A NumPy array describing the contour relationships (parent-child structure)



### `cv2.threshold()`
Is used to apply image thresholding, which means converting an image into a binary image (black and white) or segmenting pixel intensity values based on a threshold.
```python
retval, thresholded_image = cv2.threshold(src, thresh, maxval, type)
```

- `src` : Input image (must be grayscale)
- `thresh` : Threshold value (0-255)
- `maxval` : Value to assign when condition is met (e.g., 255 for white)
- `type` : Thresholding type (defines how thresholding is applied)

**Returns**
- `retval` : The applied threshold value (useful in Otsu's thresholding)
- `thresholded_image` : The output image after applying thresholding

**Types of Thresholding for `type`**

| Threshold Type            | Description                                                                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------------- |
| ``cv2.THRESH_BINARY``     | Pixels **above** the threshold are set to `maxval` (e.g., 255); others are set to `0`.                  |
| ``cv2.THRESH_BINARY_INV`` | Inverted version of `THRESH_BINARY`: pixels **below** the threshold are set to `maxval`, others to `0`. |
| ``cv2.THRESH_TRUNC``      | Pixels **above** the threshold are set to the threshold value; others remain unchanged.                 |
| ``cv2.THRESH_TOZERO``     | Pixels **below** the threshold become `0`; others remain unchanged.                                     |
| ``cv2.THRESH_TOZERO_INV`` | Inverted version of `THRESH_TOZERO`: pixels **above** the threshold become `0`.                         |

### Recommendations
Use the Canny method first, and then try to find the contours using that, rather than try to threshold the image and then find the contours of that. Because this type of thresholding (simple thresholding) has its disadvantages.


# Advanced

## Color Spaces

### `cv2.cvtColor()`
Convert an image from one color space to another
```python
dst = cv2.cvtColor(image, code[, dstCn])
```

- `image` : The input image to convert
- `code` : The color conversion code
- `dstCn`  (optional) : The number of channels in the destination image.

**Common Color Conversion Codes**

|Code|Description|
|---|---|
|`cv2.COLOR_BGR2GRAY`|Convert **BGR → Grayscale**.|
|`cv2.COLOR_BGR2RGB`|Convert **BGR → RGB**.|
|`cv2.COLOR_BGR2HSV`|Convert **BGR → HSV** (Hue, Saturation, Value).|
|`cv2.COLOR_BGR2LAB`|Convert **BGR → LAB** color space.|
|`cv2.COLOR_RGB2BGR`|Convert **RGB → BGR**.|
|`cv2.COLOR_HSV2BGR`|Convert **HSV → BGR**.|

💡 **Note:** OpenCV loads images in **BGR format** by default, not RGB.

**Examples**

```python
import cv2 as cv
import matplotlib.pyplot as plt


img = cv.imread('Photos/park.jpg')
cv.imshow('Park', img)
# BGR to Grayscale
# plt.imshow(img)
# plt.show()

gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('Gray', gray)

# BGR to HSV
hsv = cv.cvtColor(img, cv.COLOR_BGR2HSV)
cv.imshow('HSV', hsv)

# BGR to L*a*b
lab = cv.cvtColor(img, cv.COLOR_BGR2LAB)
cv.imshow('LAB', lab)

# BGR to RGB
rgb = cv.cvtColor(img, cv.COLOR_BGR2RGB)
cv.imshow('RGB', rgb)


# HSV to BGR
hsv_bgr = cv.cvtColor(hsv, cv.COLOR_HSV2BGR)
cv.imshow('HSV->BGR', hsv_bgr)

cv.waitKey(15000)
cv.destroyAllWindows()
```

>[!tip] You cannot convert grayscale image to HSV directly. Convert the grayscale to BGR and then to HSV

## Color Channels

OpenCV allows you to split an image into its respective color channels. So you can take an BGR image and split into blue, green and red components.


>[!tip] Regions where it's lighter showed that there is a far more concentrations of those pixel values and regions where it's darker, represented a little or even no pixels in that region

![[bgr channels image example.png]]


### `cv2.split()`
Separates a multi-channel image into its individual color channels. 
```python
b, g, r = cv2.split(src)
```

`src` : The source image (NumPy array with multiple channels)

**Returns** a tuple of images, each containing a single channel from the original image

**Example**
Image from the example are above
```python
import cv2 as cv
import numpy as np

img = cv.imread('Photos/park.jpg')
cv.imshow('Park', img)

b, g, r = cv.split(img)

cv.imshow('Blue', b)
cv.imshow('Green', g)
cv.imshow('Red', r)

print(f'Blue shape {b.shape}')
print(f'Green shape {g.shape}')
print(f'Red shape {r.shape}')

cv.waitKey(0)
cv.destroyAllWindows
```


#### `cv2.split()` vs NumPy Indexing

| Method         | Performance                  | Description                             |
| -------------- | ---------------------------- | --------------------------------------- |
| cv2.split()    | Slower (creates copies)      | Returns separate copies of each channel |
| NumPy indexing | Faster (views original data) | Accesses channels without copying       |
```python
import cv2 as cv
import numpy as np
import time

img = cv.imread('Photos/park.jpg')
# cv.imshow('Park', img)

def split_image(img):
    start = time.perf_counter_ns()
    b, g, r = cv.split(img)
    end = time.perf_counter_ns()
    print(f"Tiempo de ejecucion split {(end-start)} nanosegundos")
    cv.imshow('Blue', b)
    cv.imshow('Green', g)
    cv.imshow('Red', r)
    
def split_image2(img):
    start = time.perf_counter_ns()
    b = img[:, :, 0]
    g = img[:, :, 1]
    r = img[:, :, 2]
    end = time.perf_counter_ns()
    print(f"Tiempo de ejecucion slicing {(end-start)} nanosegundos")
    cv.imshow('Blue', b)
    cv.imshow('Green', g)
    cv.imshow('Red', r)

split_image(img)
split_image2(img)
```

```bash
PS C:\Users\mitch\Documents\OpenCV-Course> python splitmerge.py
Tiempo de ejecucion split 753900 nanosegundos
Tiempo de ejecucion slicing 9800 nanosegundos
```


### `cv2.merge()`

Combines separate color channels into a single multi-channel image. It is the inverse operation of `cv2.split`.

```python
dst = cv2.merge([channel1, channel2, channel3])
```

`[channel1, channel2, channel3]` : List of separate image channels (grayscale image) to be merged into a single multi-channel image.

>[!important] Order matters. The order must be [blue, green, red]. Other format will swap colors incorrectly

#### `cv2.merge()` vs NumPy Stacking

| Method        | Performance     | Description                           |
| ------------- | --------------- | ------------------------------------- |
| `cv2.merge()` | Faster          | Preferred for OpenCV image processing |
| np.dstack()   | Slightly slower | More flexible                         |

### Visualizing each Channel in Color
By default, when we display individual channels, they appear in grayscale. To visualize them in color, we need to merge the  extracted channel with empty channels

```python
import cv2 as cv
import numpy as np

img = cv.imread('Photos/park.jpg')
cv.imshow('Park', img)

blank = np.zeros(img.shape[:2], dtype='uint8')

b, g, r = cv.split(img)
blue = cv.merge([b, blank, blank])
green = cv.merge([blank, g, blank])
red = cv.merge([blank, blank, r])

cv.imshow('Blue', blue)
cv.imshow('Green', green)
cv.imshow('Red', red)
```
































---
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
