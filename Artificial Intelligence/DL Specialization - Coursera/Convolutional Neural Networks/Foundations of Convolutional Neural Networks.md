
# Computer Vision

Computer Vision Problems
 - Image Classification
 - Object Detection
 - Neural Style Transfer

>[!warning] One of the challenges of computer vision problemas is that the inputs can get really big

# Edge Detection


![[Pasted image 20250322001311.png]]
![[Pasted image 20250322002840.png]]

- python excercise: conv-forward
- TensorFlow: `tf.nn.conv2d`
- Keras: `Conv2D`

Vertical:
$$
\begin{bmatrix}
1 & 0 & -1 \\
1 & 0 & -1 \\
1 & 0 & -1 \\
\end{bmatrix}
$$

Horizontal:
$$
\begin{bmatrix}
1 & 1 & 1 \\
0 & 0 & 0 \\
-1 & -1 & -1 \\
\end{bmatrix}
$$



[[Semana 3#Operador Sobel|Sobel Filter]]
Sobel Filter
$$
\begin{bmatrix}
1 & 0 & -1 \\
2 & 0 & -2 \\
1 & 0 & -1
\end{bmatrix}
$$


Scharr filter
$$
\begin{bmatrix}
3 & 0 & 3 \\
10 & 0 & -10 \\
3 & 0 & -3
\end{bmatrix}
$$


# Padding
Is the process of adding extra pixels (usually zeros) around the input image before applying the convolution operation. 

Downsides for applying convolution multiple times
- The image shrinks
- We're throwing away information near the edge of the image

**Valid convolution**: No padding
$$
n \times n \quad * \quad f \times f \quad \to \quad (n-f+1) \times (n-f+1)
$$
**Same convolution**. Pad so that output size is the same as the input size
$$
(n + 2p -f+1) \times (n +2p-f+1)
$$


# Stride Convolutions
The filter moves across the input with a step $s$ size greater than one. This reduces the spatial dimensions of the output.

![[Pasted image 20250322095920.png]]
![[Pasted image 20250322095958.png]]

### Summary of convolutions
- $n \times n$ image , $f \times f$ filter
- padding $p$
- stride $s$

The output dimensions 
$$
\lfloor \dfrac{n+2p-f}{s} + 1 \rfloor \ \times \ \lfloor \dfrac{n+2p-f}{s} + 1 \rfloor
$$


[[Semana 3#Correlación vs Convolución|cross-correlation vs. convolution]]

# Convolutions Over Volume
![[Pasted image 20250322102049.png]]
To compute the output at position (0,0), place de $3 \times 3 \times 3$ filter at the top-left corner of the input.The filter has 27 values, corresponding to a 3D cube covering all three color channels. Multiply each filter value by the corresponding pixel in the red, green, and blue channels, sum all 27 products, and the result becomes the first output value.


![[Pasted image 20250322102130.png]]

**Summary**
$$
(n \times n \times n_c) \ * \ (f \times f \times n_c) \to (n-f+1) \times (n-f+1) \times n'_c
$$
where $n'_c$ is the number of filters

**Example**
For two filters, $n'_c=2$
$$
(6 \times 6 \times 3 ) \ * \ (f \times f \times n_c) \ \to \ (4 \times 4 \times 2)
$$

# One Layer of a Convolution Net
![[Pasted image 20250322124732.png]]

# Simple Convolutional Network Example

![[Pasted image 20250323003849.png]]

Types of layer in a convolutional network
- Convolution
- Pooling
- Fully connected

# Pooling layer

>[!note] Pooling has  a set of hyperparameters but it has no parameters to learn. It's just a fixed computation

## Max pooling
Each of the outputs will just be the max from the corresponding reshaded region
![[Pasted image 20250323005027.png]]

## Average pooling
![[Pasted image 20250323111930.png]]

### Summary of pooling

**Hyperparameters:
- f: filter size
- s: string
- Max or average pooling
- p: padding (rarely used)



# Convolutional Neural Network Example

![[Pasted image 20250323113159.png]]