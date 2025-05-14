[Computer Vision codes.ipynb - Colab](https://colab.research.google.com/drive/1a0Bqacodk5o8Byx_6gLrC1bUt5WCFgGW#scrollTo=ISKDBxjfLQtf)


# Gaussian Filter

The **Gaussian filter** is based on the **Gaussian function**, a bell-shaped probability distribution. It is used to compute a weighted average of pixel values within a local neighborhood, where pixels closer to the center of the filter contribute more to the final computed value.

The mathematical formula for the **Gaussian distribution** is:

$$f(x, y) = \frac{1}{2 \pi \sigma^2} \exp \left( -\frac{x^2 + y^2}{2 \sigma^2} \right)$$

Where:

- $f(x, y)$ represents the function value at coordinates (x,y)(x, y).
    
- $\sigma$ is the **standard deviation**, which controls the "spread" of the Gaussian curve—determining how smooth or concentrated the blur effect will be.
    
- $x$ and $y$ represent the relative distances from the filter’s center.


This filtering technique is commonly used in **image smoothing** to reduce noise while preserving important structures.


# Box filtering
Each pixel in the output image is computed as the average of the surrounding pixels in a rectangular region.

**Example: 3×3 Kernel**

Let's take a **3×3** kernel and apply it to a grayscale image:

Original Pixel Values:

```
120  125  130
140  150  160
170  175  180
```

Applying a 3×3 Average Blur:

Each pixel is replaced by the **average** of itself and its neighbors. For example, the new value of the center pixel `150` is:

$$
\frac{120 + 125 + 130 + 140 + 150 + 160 + 170 + 175 + 180}{9} = 150$$

The same operation is applied to every pixel, creating a **blurry effect**.

# Canny Edge Detection
Is a popular edge detection algorithm. It is a multi-stage algorithm:

1. **Noise Reduction**
2. **Finding Intensity Gradient of the Image**
3. **Applying Non-Maximum Suppression**
4. **Hysteresis Thresholding**


## Noise Reduction
Since edge detection is susceptible to noise in the image, first step is to remove the noise in the image with a 5x5 [[#Gaussian Filter]].

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


## Hysteresis Thresholding
This stage decides which are all edges are really edges and which are not. For this, we need two threshold values, minVal and maxVal. Any edges with intensity gradient more than maxVal are sure to be edges and those below minVal are sure to be non-edges, so discarded. Those who lie between these two thresholds are classified edges or non-edges based on their connectivity. If they are connected to "sure-edge" pixels, they are considered to be part of edges. Otherwise, they are also discarded. See the image below:

![](https://docs.opencv.org/4.x/hysteresis.jpg)

The edge A is above the maxVal, so considered as "sure-edge". Although edge C is below maxVal, it is connected to edge A, so that also considered as valid edge and we get that full curve. But edge B, although it is above minVal and is in same region as that of edge C, it is not connected to any "sure-edge", so that is discarded. So it is very important that we have to select minVal and maxVal accordingly to get the correct result.

This stage also removes small pixels noises on the assumption that edges are long lines.

So what we finally get is strong edges in the image.


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



# The Laplacian operator

$$
L(x, y) = \dfrac{\partial^2 I}{\partial x^2} + \dfrac{\partial^2 I}{\partial y^2}
$$
The sum of these derivatives highlights regions of rapid intensity changes (edges).

A common kernel used for the Laplacian operator is:

$$\begin{bmatrix} 0 & 1 & 0 \\ 1 & -4 & 1 \\ 0 & 1 & 0 \end{bmatrix}​$$

or another version:

$$\begin{bmatrix} 1 & 1 & 1 \\ 1 & -8 & 1 \\ 1 & 1 & 1 \end{bmatrix}​$$

These kernels sum the differences of pixel intensities around a central pixel to detect **sharp changes** (edges).


# **📌 Sobel Operator**

The **Sobel operator** is an edge detection filter that computes the **partial derivatives** of an image in both the **X (horizontal)** and **Y (vertical)** directions. These derivatives are combined to obtain the **gradient magnitude**, which highlights the edges in an image.

Sobel filters use **convolution masks (kernels)** to approximate the first-order derivatives of an image. In other words, the operator measures the **rate of intensity change** in both directions, allowing us to detect edges.

---

## **📌 Sobel Kernels (Filter Masks)**

The **Sobel kernels** for detecting gradients in the X and Y directions are as follows:

### **Kernel in the X-direction (GxG_x)**

Gx=[10−120−210−1]G_x = \begin{bmatrix} 1 & 0 & -1 \\ 2 & 0 & -2 \\ 1 & 0 & -1 \end{bmatrix}

This kernel detects **vertical edges** (changes in intensity along the X-axis).

### **Kernel in the Y-direction (GyG_y)**

Gy=[121000−1−2−1]G_y = \begin{bmatrix} 1 & 2 & 1 \\ 0 & 0 & 0 \\ -1 & -2 & -1 \end{bmatrix}

This kernel detects **horizontal edges** (changes in intensity along the Y-axis).

After applying these filters to an image, they highlight intensity variations in the horizontal and vertical directions.

---

## **📌 Computing the Gradient Magnitude**

The **gradient magnitude** represents the strength of the edge at each pixel and is computed using the following formula:

G=Gx2+Gy2G = \sqrt{G_x^2 + G_y^2}

This value determines the edge intensity at a given point in the image.

---

## **📌 Steps to Apply the Sobel Filter to an Image (512x512)**

1. **Convert the image to grayscale.**
    
2. **Define the Sobel kernels** GxG_x and GyG_y.
    
3. **Create an empty matrix** to store the result.
    
    - A new **512×512** matrix is required to store the processed image.
        
4. **Iterate through the image while applying the Sobel filter**:
    
    - Since the kernels are **3×3**, we must process **each pixel** from **(1,1) to (510,510)** (excluding the borders).
        
    - For each pixel **(i, j)**:
        
        1. Extract a **3×3 window** centered at **(i, j)**.
            
        2. Multiply this window **element-wise** with GxG_x and GyG_y.
            
        3. Sum the results to obtain SxS_x and SyS_y.
            
        4. Compute the **gradient magnitude**:
            
            G=Sx2+Sy2G = \sqrt{S_x^2 + S_y^2}
        5. Assign GG to the new image matrix.
            
5. **Normalize the pixel values**:
    
    - The resulting values might exceed the range **[0, 255]**, so normalization is required.
        
6. **Return the final edge-detected image.**
    

---

## **📌 Python Implementation of Sobel Edge Detection**

The following function implements the **Sobel operator** using **NumPy**:

```python
import cv2
import numpy as np

def sobel_edge_detection(image):
    """
    Applies the Sobel edge detection filter to a grayscale image.

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
    
    G_x = np.array([[-1,  0,  1],
                    [-2,  0,  2],
                    [-1,  0,  1]])
    
    # Get the image dimensions
    M, N = image.shape

    # Initialize an empty matrix to store the gradient magnitudes
    im_border = np.zeros((M, N))

    # Iterate over the image, avoiding the borders
    for i in range(1, M-1):
        for j in range(1, N-1):
            sub_image = image[i-1:i+2, j-1:j+2]  # Extract 3×3 window
            S_x = np.sum(G_x * sub_image)  # Compute convolution with G_x
            S_y = np.sum(G_y * sub_image)  # Compute convolution with G_y
            G = np.sqrt(S_x**2 + S_y**2)  # Compute gradient magnitude
            im_border[i, j] = G

    # Alternative approach using OpenCV's filter2D
    filter_X = cv2.filter2D(image, -1, G_x)
    filter_Y = cv2.filter2D(image, -1, G_y)
    im_border = np.sqrt(filter_X**2 + filter_Y**2)

    # Normalize the image to scale values between 0 and 255
    min_val, max_val = np.min(im_border), np.max(im_border)
    im_border = 255 * (im_border - min_val) / (max_val - min_val)

    return im_border.astype(np.uint8)  # Convert back to 8-bit format
```

---

## **📌 Alternative: Using OpenCV's Built-in Sobel Function**

The same operation can be performed using OpenCV’s built-in **cv2.Sobel()** function:

```python
# Read the image and convert to grayscale
img = cv2.imread("Photos/cats.jpg")
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Apply Sobel filter in X and Y directions
sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3)  # Horizontal edges
sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3)  # Vertical edges

# Convert to absolute values and scale to 8-bit format
sobel_x = cv2.convertScaleAbs(sobel_x)
sobel_y = cv2.convertScaleAbs(sobel_y)

# Combine the gradients
sobel_combined = cv2.bitwise_or(sobel_x, sobel_y)

# Display the results
cv2.imshow("Sobel X", sobel_x)
cv2.imshow("Sobel Y", sobel_y)
cv2.imshow("Sobel Combined", sobel_combined)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

## **📌 Key Takeaways**

✅ **Sobel detects edges by computing the gradient in X and Y directions.**  
✅ **It is less sensitive to noise than a simple derivative filter.**  
✅ **Kernel size affects the smoothness of detected edges.**  
✅ **Combining both Sobel-X and Sobel-Y enhances edge detection.**

Would you like a visual explanation of the Sobel operator step by step? 🚀
