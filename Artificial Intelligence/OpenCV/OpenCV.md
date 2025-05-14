

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
Using the [[#Advanced#`cv2.cvtColor()`|cv2.cvtColor()]] method 
```python
# Coverting to grayscale
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('Gray', gray)
```

### Blurring an image
Using the [[#Advanced#`cv2.GaussianBlur()`|cv2.GaussianBlur]] method 
```python
# Blur
blur = cv.GaussianBlur(img, (5, 5), cv.BORDER_DEFAULT)
cv.imshow('Blur', blur)
```


### Edge cascade
Using [[#`cv2.Canny()`]]

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


### Example

```python
import cv2 as cv
import numpy as np

img = cv.imread('Photos/cats.jpg')
cv.imshow('Cats', img)

blank = np.zeros(img.shape, dtype='uint8')
cv.imshow('Blank', blank)


gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('Gray', gray)

# blur = cv.GaussianBlur(gray, (5,5), cv.BORDER_DEFAULT)

canny = cv.Canny(gray, 125, 175)
cv.imshow('Canny', canny)

# Thresholding
ret, thresh = cv.threshold(gray, 125, 255, cv.THRESH_BINARY)
cv.imshow('Thresh', thresh)

contours, hierarchies = cv.findContours(thresh, cv.RETR_LIST, cv.CHAIN_APPROX_SIMPLE)
print(f'{len(contours)} contour(s) found')

cv.drawContours(blank, contours, -1, (0,0,255), 2)
cv.imshow('Contours drawn', blank)

cv.waitKey(0)
cv.destroyAllWindows()
```


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



## Blurring techniques

### `cv2.blur()`
Applies a normalized [[Computer Vision Theory#Box filtering|box filter]] to an image, which results in a simple averaging blur effect. This means that each pixel in the output image is replaced by the average of the pixel values in its surrounding neighborhood.

```python
cv2.blur(src, ksize, dst=None, anchor=(-1, -1), borderType=cv2.BORDER_DEFAULT)
```

- `src` : The input image
- `ksize` : The kernel size `(width, height)` , which defines the neighborhood used for averaging.
- `dst` (optional) : Output image (same size as input). If not provided, OpenCV creates one
- `anchor` (optional) : The anchor point withing the kernel. `(-1, -1)` means the center of the kernel.
- `borderType`  (optional) : Border handling mode. Defines how pixels outside the image boundaries are handled

### `cv2.GaussianBlur()`
Is used to apply a [[Computer Vision Theory#Filtro gaussiano|Gaussian blur]] to an image. This helps in reducing noise, smoothing the image, and improving edge detection.
Gaussian blur works by applying a Gaussian kernel (a bell-shaped function) to each pixel and its neighbors, giving more weight to the central pixel and less weight to distant ones.

```python
blur_image = cv2.GaussianBlur(src, ksize, sigmaX[, dst[, sigmaY[, borderType]]])
```

- `src` : The input image to blur
- `ksize` : The size of the kernel (odd number, e.g., `(5,5)`). 
- `sigmaX` : Standard deviation in the $X$ direction (controls the blur amount)
	- `1` : light blur
	- `3` : stronger blur
	- `0` : OpenCV automatically selects `sigmaX`
- `dst` (optional) : Output image. If not provided, OpenCV creates one
- `sigmaY` (optional) : Standard deviation in the $Y$-direction. If `0` is set equal to `sigmaX`
- `borderType` (optional) : Defines how edges are handled (default `cv2.BORDER_DEFAULT`)
    - `cv2.BORDER_CONSTANT`: Rellenar con un valor constante (por defecto 0).
    - `cv2.BORDER_REFLECT`: Reflejar los píxeles en los bordes.
    - `cv2.BORDER_REPLICATE`: Replicar los píxeles del borde.

>[!tip] The larger the kernel, the more blurred the image will be.

**Example: 3x3 Gaussian Kernel**
A Gaussian kernel of size 3x3 might look like this

$$
\begin{matrix}
1 & 2 & 1 \\
2 & 4 & 2 \\
1 & 2 & 1
\end{matrix}
$$



### `cv2.medianBlur(src, ksize)`
Applies median blurring, which is highly effective in reducing noise while preserving edges. Instead of averaging pixel values (as `cv2.blur()` or `cv2.GaussianBlur()`), median blurring replaces each pixel with the median of the surrounding pixels.

```python
cv2.medianBlur(src, ksi)
```

- `ksize` : Size of the square kernel (must be an odd number).

**Steps**
1. A square kernel of size `ksize x ksize` is placed over each pixel
2. All pixel values inside the kernel are sorted in ascending order
3. The center pixel is replaced with the median value of the sorted list
4. This process is repeated for every pixel in the image

**Example with a 3x3 kernel**
Before Applying `medianBlur()`

$$
\begin{matrix}
120 & 125 & 130 \\
100 & 110 & 140 \\
90 & 95 & 200
\end{matrix}
$$

Sorted values: $[90, 95, 100, 110, 120, 125, 130, 140, 200]$
- Median value = 120
- The center pixel (110) is replaced by 120

**Uses**
- Great for removing salt-and-pepper noise
- Preserves edges better than other blurring technique


### `cv2.bilateralFilter()`
Is an edge-preserving smoothing technique that reduces noise while keeping sharp edges intact. It is more advanced than Gaussian or median blurring because it considers both spatial and intensity differences when smoothing an image.

```python
cv2.bilateralFilters(src, d, sigmaColor, sigmaSpace, borderType=cv2.BORDER_DEFAULT)
```

- `src` : Input image
- `d` : Diameter of the pixel neighborhood used for filtering
- `sigmaColor` : How much colors should be mixed. Higher values mean more color smoothing. 
- `sigmaSpace` : How much influence nearby pixels have. Higher values mean larger smoothing areas. 
- `borderType` (optional) : Specifies how image borders are handled (default is `cv2.BORDER_DEFAULT`)

>[!iinfo] `sigmaColor`
>- Defines how sensitive the filter is to color differences
>- Higher values mean that more distant intensities are considered similar, allowing stronger smoothing.
>- Lower values mean only very similar colors are blended, preserving details better

>[!info] `sigmaSpace`
>- Defines how far neighboring pixels can influence the filtering
>- Higher values allow farther pixels to contribute, leading to stronger but slower smoothing
>- Lower values restrict filtering to only close neighbors, preserving small textures



### Blurring Techniques in OpenCV


| Blurring Method         | Key Properties                                 | Best Use Case                                                                          |
| ----------------------- | ---------------------------------------------- | -------------------------------------------------------------------------------------- |
| `cv2.blur()`            | Simple, fast, but blurs edges                  | Basic noise reduction                                                                  |
| `cv2.GaussianBlur()`    | Weighted blur, softer effect                   | Pre-processing for edge detection                                                      |
| `cv2.medianBlur()`      | Removes salt-and-pepper noise, preserves edges | Noise removal while keeping details (Slower than Gaussian blur for large kernel sizes) |
| `cv2.bilateralFilter()` | Smooths while preserving edges                 | High-quality image enhancement (Computationally espensive)                             |


## BITWISE Operations

- AND 
- OR 
- XOR 
- NOT
Bitwise operators operate in a binary manner. So a pixel is turned off if it has a value of zero, and is turned on if it has a value of one.

### `cv2.bitwise_and()`
Performs a pixel-wise `AND` operation between two images or between an image and a mask

```python
result = cv2.bitwise_and(src1, src2, dst=None, mask=None)
```

- `src1`, `src2` : First and second input image (same size and type)
- `dst` (optional) : Output image (same size & type as inputs). If not provided, a new array is created
- `mask` (optional) : Binary mask (white areas define the region where `AND` is applied)

**Returns**
A new image where the `AND` operation has been applied


### `cv2.bitwise_or()`
Performs a pixel-wise `OR` operation between two images or between an image and a mask.
```python
result = cv2.bitwise_or(src1, src2, dst=None, mask=None)
```

Same parameters as `cv2.bitwise_and`

### `cv2.bitwise_or()`
Performs a pixel-wise `XOR` operation between two images or between an image and a mask.
```python
result = cv2.bitwise_xor(src1, src2, dst=None, mask=None)
```

Same parameters as `cv2.bitwise_and`


### `bitwise_not`
Performs a bitwise `NOT` operation on an image, meaning it inverts all pixels values
```python
dst = cv2.bitwise_not(src, mask=None)
```

- `src`:  Same as other bitwise methods
- `mask`: Same as other bitwise methods


### Example

![[bitwise examples.png]]
## Masking
Masking essentially allows us to focus on certain parts of an image that we'd like to focus on.

Masking is a technique in image processing where a binary mask (a grayscale image with values 0 or 255) is applied to another image to selectively process or highlight specific regions while ignoring others.

**Steps**
1. Start with an original image
2. Create a mask
	- Can be a simple **black-and-white shape**.
	- Can be based on **thresholding** (e.g., selecting bright regions).
	- Can be manually drawn **ROI**
3. Apply a bitwise operation (e.g., `cv2.bitwise_and()`) using the mask


**Example**
```python
import cv2 as cv
import numpy as np

img = cv.imread('Photos/cats.jpg')
cv.imshow('Cats', img)


mask = np.zeros(img.shape[:2], dtype='uint8')
#cv.imshow('Blank image', blank)

mask = cv.circle(mask, (img.shape[1] // 3, img.shape[0] // 3), 100, 10, -1)
mask = cv.rectangle(mask, (img.shape[1] // 2, img.shape[0] // 2), ((img.shape[1] // 2) + 150, (img.shape[0] // 2) + 150), 50, -1)
cv.imshow('Mask', mask)

masked = cv.bitwise_and(img, img, mask=mask)
cv.imshow('Masked AND', masked)

masked_or = cv.bitwise_or(img, img, mask=mask)
cv.imshow('Masked OR', masked_or)

masked_xor = cv.bitwise_xor(img, img, mask=mask)
cv.imshow('Masked XOR', masked_xor)

cv.waitKey(0)   
```

![[masking examples.png]]


>[!tip] In bitwise operations the mask is treated as a binary mask
>- Pixels with values `0` are ignored (black = completely masked out)
>- Pixels with values `> 0` are treated as 255 (white = fully applied)


## Computing histograms

Histograms basically allow you to visualize the distribution of pixel intensities in an image. So whether it's a color image, or whether it's a grayscale image, you can visualize these pixels intensity distributions with the help of an histogram.

A histogram is a graphical representation of the distribution of pixel intensities in an image. It tells us how many pixels hace a specific intensity value.

- For grayscale images, a histogram typically has 256 bins (one for each intensity)
- For color images (RGB), we can have three separate histograms, one for each channel

>[!tip] **Bins** represent intervals (or ranges) of pixel intensity values.

**Importance**
1. **Understanding Image Brightness & Contrast** - Helps determine if an image is too dark, too bright, or well-balanced.
2. **Image Enhancement** - Used in techniques like histogram equalization to improve contrast
3. **Thresholding & Segmentation** - Help choose optimal threshold values.
4. **Feature Extraction** - Used in object detection and image classification.


### `cv2.calcHist()`
Is used to calculate the histogram of an image.
```python
cv2.calcHist(images, channels, mask, histSize, ranges[, accumulate])
```

**Returns**
A NumPy array representing the histogram values

- `images` : List containing the image in grayscale or RGB. It must be enclosed in brackets.
- `channels` : Specifies which channel to analyze: `0` for grayscale or B: 0, G: 1, R: 2 for color images.
- `mask` (optional) : A binary mask to compute the histogram for a specific region in the image. Use `None` for the full image.
- `histSize` : The number of bins (intervals) for the histogram (e.g., `[256]` for grayscale or `[32]` for color).
- `ranges` : The intensity range to consider: `[0, 256]` for grayscale (converting 0-255 pixel values).
- `acumulate` : If `True`, accumulates histogram values over multiple calls instead of resetting. Default is `False`.


**Example**

![[histogram examples.png]]

## Thresholding

Thresholding is a technique in image processing used to separate objects from the background by converting a grayscale image into a binary image.

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


### `cv2.adaptiveThreshold()`
Applies adaptive thresholding
```python
dst = cv2.adaptiveThreshold(src, maxValue, adaptiveMethod, thresholdType, blockSize, c)
```

- `src` : Input grayscale image (must be single-channel).
- `maxValue` : The pixel assigned to pixels that meet the threshold condition (usually 255 for white).
- `adaptiveMethod` : The method used to compute the local threshold.
- `thresholdType` : The type of thresholding (e.g., `cv2.THRESH_BINARY` )
- `blockSize` : The size of the neighborhood used to calculate the threshold for each pixel (must be an odd number)
- `C` : A constant subtracted from the computed threshold value to fine-tune the result.

**Types of `adaptiveMethod`**

| Method                              | Description                                                                                   |
| ----------------------------------- | --------------------------------------------------------------------------------------------- |
| `cv2.ADAPTIVE_THRESH_MEAN_C`        | The threshold value is the mean of the neighboring pixel values                               |
| `cv2.ADAPTIVE_THRESHOLD_GAUSSIAN_C` | The threshold value is a weighted sum of the neighboring pixel values using a Gaussian window |

**Types of `thresholdType`**

| Type                    | Description                                                            |
| ----------------------- | ---------------------------------------------------------------------- |
| `cv2.THRESH_BINARY`     | Pixels above the computed threshold are set to `maxValue`, others to 0 |
| `cv2.THRESH_BINARY_INV` | Pixels above the computed threshold are set to 0, others to `maxValue` |


### Examples

![[example threshold.png]]

## Edge Detection

### `cv2.Laplacian()`

[[Computer Vision Theory#The Laplacian operator]]

The **Laplacian operator** is a second-order derivative filter used for **edge detection**. Unlike Sobel, which computes gradients in one direction at a time (horizontal or vertical), Laplacian computes the **sum of second-order derivatives in all directions**, making it more sensitive to rapid intensity.

```python
cv2.Laplacian(src, ddepth[, ksize[, scale[, delta[, borderType]]]])
```

- `src` : Input image
- `ddepth` : Desired depth of the output image (e.g., `cv2.CV_64F`) to keep negative values).
- `ksize` (optional) : Aperture size of the kernel (must be an odd number). Default: `1`.
- `scale` : Scaling factor for the computed Laplacian values. Default: `1`.
- `delta` : Value added to the result before storing it in `dst`. Default: `0`.
- `borderType` : How the image borders are handled (e.g., `cv2.BORDER_DEFAULT`).


**Ejemplo**

```python
import cv2 as cv
import numpy as np

img = cv.imread('Photos/cats.jpg')

gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('Gray', gray)

# Appy the laplacian operator (using 64-bit float to preserve negative values)
laplacian = cv.Laplacian(gray, cv.CV_64F)

# Convert to uint8 for proper display
laplacian = np.uint8(np.absolute(laplacian))
# Also works with (recommended)
# laplacian = cv.convertScaleAbs(laplacian)

cv.imshow('Laplacian', laplacian)

cv.waitKey(0)

```



### `cv2.Sobel()`

[[Computer Vision Theory#**📌 Sobel Operator**]]

The `cv2.Sobel()` function in OpenCV is used for **edge detection** by computing the first-order derivatives (gradients) of an image. It is an improvement over the **Sobel operator**, which is a discrete differentiation operator that calculates an approximation of the gradient of the image intensity function.

```python
dst = cv2.Sobel(src, ddepth, dx, dy, ksize[, scale[, delta[, borderType]]])
```


- **`src`**: Input image (grayscale or color).
- **`ddepth`**: Desired depth of the output image. Usually `cv2.CV_64F` or `cv2.CV_32F` for better precision.
- **`dx`**: Order of the derivative in the **x-direction** (1 for first derivative, 2 for second derivative).
    - To detect horizontal edges `dx = 1` y `dy = 0`.
    - To detect vertical edges `dx = 0` y `dy = 1`.
- **`dy`**: Order of the derivative in the **y-direction** (1 for first derivative, 2 for second derivative).
- **`ksize`**: Size of the Sobel kernel (must be **odd**). Larger values detect larger edges but can cause blurring.
- **`scale`** (optional): Scaling factor for the computed gradient values (default = `1`).
- **`delta`** (optional): Value added to the computed gradient values (default = `0`).
- **`borderType`** (optional): Specifies how to handle image borders (default = `cv2.BORDER_DEFAULT`).


**Example**
```python
import cv2 as cv
import numpy as np

# Load the image
img = cv.imread('Photos/cats.jpg', cv.IMREAD_GRAYSCALE)

# Compute Sobel gradients in x and y directions
sobelx = cv.Sobel(img, cv.CV_64F, 1, 0, ksize=3)  # Detects vertical edges
sobely = cv.Sobel(img, cv.CV_64F, 0, 1, ksize=3)  # Detects horizontal edges

# Convert to absolute values and scale to uint8
sobelx = cv.convertScaleAbs(sobelx)
sobely = cv.convertScaleAbs(sobely)

# Combine both gradients
sobel_combined = cv.bitwise_or(sobelx, sobely)

# Display results
cv.imshow('Original', img)
cv.imshow('Sobel X', sobelx)
cv.imshow('Sobel Y', sobely)
cv.imshow('Sobel Combined', sobel_combined)

cv.waitKey(0)
cv.destroyAllWindows()

```


### `cv2.Canny()`
Is used to detect edges in an image using the **[[Computer Vision Theory#Canny Edge Detection|Canny Edge Detection algorithm]]** .
```python
cv2.Canny(image, threshold1, threshold2)
```


- `src` : The input image (must be a **grayscale** image).
- `threshold1` : The **lower threshold** for the [[Computer Vision Theory#Canny Edge Detection#Hysteresis Thresholding|hysteresis thresholding process]] .
- `threshold2` : The **upper threshold** for the [[Computer Vision Theory#Canny Edge Detection#Hysteresis Thresholding|hysteresis thresholding process]].
- `edges` (optional) : Output image where detected edges will be stored.
- `apertureSize` (optional) : Size of the Sobel kernel used for gradient calculation.
- `L2gradient` (optional) : If `True`, computes gradient magnitude using the **L2 norm** (Euclidean distance). If `False`, uses the **L1 norm** (sum of absolute differences).


| Lower (threshold1)        | Upper (threshold2)          | Effect                                                                     |
| ------------------------- | --------------------------- | -------------------------------------------------------------------------- |
| **Low** (e.g., `50`)      | **High** (e.g., `150`)      | ✅ **Good balance**, detects strong edges and keeps weak ones if connected. |
| **Low** (e.g., `30`)      | **High** (e.g., `200`)      | 🔍 **More edges**, but may increase noise.                                 |
| **High** (e.g., `100`)    | **Very High** (e.g., `200`) | ✂ **Fewer edges**, only detects strong ones.                               |
| **Very Low** (e.g., `10`) | **Very High** (e.g., `250`) | ❌ **Too many edges**, lots of noise.                                       |

**🔹 Rule of Thumb:** `threshold2 ≈ 2 × threshold1` (but this varies by image).




# Otros

## `borderType`
Is a parameter in many OpenCV functions that defines how the image border is handled when applying filters or transformations.


| Border Type                                      | Description                                                              |
| ------------------------------------------------ | ------------------------------------------------------------------------ |
| `cv2.BORDER_CONSTANT`                            | Pads with a constant value (default is black if not especified)          |
| `cv2.BORDER_REPLICATE`                           | Extends the edge pixel outward                                           |
| `cv2.BORDER_REFLECT`                             | Mirrors the image at the edge                                            |
| `cv2.BORDER_REFLECT_101` (also `BORDER_DEFAULT`) | Like `BORDER_REFLECT`, but does not repeat the edge pixel                |
| `cv2.BORDER_WRAP`                                | Wraps around the image (left border comes from the right and vice versa) |
| `cv2.BORDER_ISOLATED`                            | Ignores border pixels during operations                                  |
| `CV2.BORDER_TRANSPARENT`                         | Leaves the border area unchanged                                         |


### `cv2.convertScaleAbs()`
Is used to scale, shift, and convert an image (or array) to an **8-bit unsigned integer** (`uint8`) while preserving the absolute values.

```python
dst = cv2.convertScaleAbs(src[, alpha[, beta]])
```

- `src` : Input image or array (can have negative values).
- `alpha` : Scale factor (default = 1). Multiplies `src` values.
- `beta` :  Shit value (default = 0). Adds a constant to `src`.

#### Why use `cv2.convertScaleAbs()` instead of `np.uint(8)`?

- `np.uint8()` **simply truncates** values outside the range [0, 255], which may **lead to incorrect results**.
    
- `cv2.convertScaleAbs()` **takes absolute values and properly scales them**, avoiding artifacts in edge detection.









---



