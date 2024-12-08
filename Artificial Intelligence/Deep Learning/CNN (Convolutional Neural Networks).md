[An Introduction to Convolutional Neural Networks: A Comprehensive Guide to CNNs in Deep Learning | DataCamp](https://www.datacamp.com/tutorial/introduction-to-convolutional-neural-networks-cnns)

<div style="text-align: center;">
<figure>
<img src=""  alt=""/>
<figcaption>
</figcaption>
</figure>
</div>

A Convolutional Neural Netowork (CNN), also know as ConvNet, is a specialized type of deep learning algorithm mainly designed for task that necessitate object recognition, including image classification, detection, and segmentation.

- CNNs are distinguished from classic machine learning algorithms such as **SVMs** and **decision trees** by their ability to autonomously extract features at large scale, bypassing the need for manual feature engineering and thereby enhancing efficiency
- The convolutional layers grant CNNS their translation-invariant characteristics, empowering them to identify and extract patterns and features from data irrespective of variations in position, orientation, scale, or translation.
- A variety of pre-trained CNN architectures, including **VGG-16**, **ResNet50**, **Inceptionv3**, and **EfficientNet**, have demonstrated top-tier performance. These models can be adapted to new task with relatively little data through a process know as fine-tuning
- Beyon image classification tasks, CNNs are versatile and can be applied to a range of other domains, such as natural language processing, time series analysis, and speech recognition


# Key Components of a CNN
The convolutional neural network is made of four main parts.
- Convolutional layers
- Rectified Linear Unit ([[Neural Networks#Funciones de activación#ReLU|ReLU]]) 
- Pooling layers
- Fully connected layers

<div style="text-align: center">
<figure>
<img src="https://media.datacamp.com/legacy/v1700043905/image10_f8b261ebf1.png"  alt=""/>
<figcaption>Achitecture of the CNNs applied to digit recognition</figcaption>
</figure>
</div>

# Convolution layers
This is the first building block of a CNN. The main mathematical task performed is called convolution, which is the application of a sliding window function to a matrix of pixel representing an image. The sliding function applied to the matrix is called **kernel** or **filter**, and both can be used interchangeably.

In the convolution layer, several filters of equal size are applied, and each filter is used to recognize a specific pattern from the image, such as the curving of the digits, the edge, the whole shape of the digits, and more.

For example, one filter might be good at finding straight lines, another might find curves, and so on. By using several different filters, the CNN can get a good idea of all the different patterns that make up the image.

Let's consider this 32x32 grayscale image of handwritten digit. 

<div style="text-align: center">
<figure>
<img src="https://media.datacamp.com/legacy/v1700043954/image5_b9b4c3cb25.png"  alt=""/>
<figcaption>Illustration of the input image and its pixel representation_</figcaption>
</figure>
</div>
The kernel used for the convolution it's a matrix with a dimension of 3x3. The weights of each element of the kernel is represented in the grid. Zero weights are represented in the black grids and ones in the white grid.

>[!info] In real life, the weights of the kernels are determined during the training process of the neural network

Using these two matrices, we can perform the convolution operation by applying the dot product, and work as follows:

1. Apply the kernel matrix from the top-left corner to the right.
2. Perform element-wise multiplication.
3. Sum the values of the products.
4. The resulting value corresponds to the first value (top-left corner) in the convoluted matrix.
5. Move the kernel down with respect to the size of the sliding window.
6. Repeat steps 1 to 5 until the image matrix is fully covered.

The dimension of the convoluted matrix depends on the size of the sliding window. The higher the sliding window, the smaller the dimension.

<div style="text-align: center">
<figure>
<img src="https://media.datacamp.com/legacy/v1700043998/image9_fbc98b6c6e.png"  alt=""/>
<figcaption>Application of the convolution task using a stride of 1 with 3x3 kernel</figcaption>
</figure>
</div>


Another name associated with the kernel in the literature is feature detector because the weights can be fine-tuned to detect specific features in the input image.

For instance:
- Averaging neighboring pixels kernel can be used to blur the input image.
- Subtracting neighboring kernel is used to perform edge detection.

The more convolution layers the network has, the better the layer is at detecting more abstract features.












