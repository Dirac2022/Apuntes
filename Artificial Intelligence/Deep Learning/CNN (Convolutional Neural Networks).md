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
- Rectified Linear Unit ([[Artificial Intelligence/Neural Networks#Funciones de activación#ReLU|ReLU]]) 
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

# Activation function
A [[Artificial Intelligence/Neural Networks#Funciones de activación#ReLU|ReLU]] activation function is applied after each convolution operation. This function helps the network learn non-linear relationships between the features in the image, hence making the network more robust for identifying different patterns. 

# Pooling Layer
The goal of the pooling layer is to pull the most significant features from the convoluted matrix. This is done by applying some aggregation operations, which reduce the dimension of the feature map (convoluted matrix), hence reducing the memory used while training the network. Pooling is also relevant for mitigating overfitting.

 Some common aggregation functions:
 - **Max pooling**, which is the maximum value of the feature map
 - **Sum pooling** corresponds to the sum of all the values of the feature map
 - **Average pooling** is the average of all the values

<div style="text-align: center">
<figure>
<img src="https://media.datacamp.com/legacy/v1700044050/image4_332794a93a.png"  alt=""/>
<figcaption>Application of max pooling with a stride of 2 using 2x2 filter</figcaption>
</figure>
</div>

Also, the dimension of the feature map becomes smaller as the pooling function is applied.

The last pooling layer flattens its feature map so that it can be processed by the fully connected layer.

# Fully connected layers
These layers are in the last layer of the convolutional neural network, and their inputs correspond to the flattened one-dimensional matrix generated by the last pooling layer.  [[Artificial Intelligence/Neural Networks#Funciones de activación#ReLU|ReLU]] activations functions are applied to them for non-linearity.

Finally, a [[Artificial Intelligence/Neural Networks#Funciones de activación#Softmax|Softmax]] prediction layer is used to generate probability values for each of the possible output labels, and the final label predicted is the one with the highest probability score.


	# Overfitting and Regularization in CNNS
This can be observed when the performance on training data is too low compared to the performance on validation or testing data, and a graphical illustration is given below:

<div style="text-align: center">
<figure>
<img src="https://media.datacamp.com/legacy/v1700044100/image3_93b1b7c0d9.png"  alt=""/>
<figcaption>Underfitting vs Overfitting</figcaption>
</figure>
</div>

Deep learning models, especially Convolutional Neural Networks (CNNs), are particularly susceptible to overfitting due to their capacity for high complexity and their ability to learn detailed patterns in large-scale data.

Several regularization techniques can be applied to mitigate overfitting in CNNs, and some are illustrated below

<div style="text-align: center">
<figure>
<img src="https://media.datacamp.com/legacy/v1700044137/image8_278eca4d24.png"  alt=""/>
<figcaption>_7 strategies to mitigate overfitting in CNNs_</figcaption>
</figure>
</div>

- **Dropout:** This consist of randomly dropping some neurons during the training process, which forces the remaining neurons to learn new features from the input data.
- **Batch normalization:** The overfitting is reduced at some extend by normalizing the input layer by adjusting and scaling the activations. This approach is also used to speed up and stabilize the training process.
- **Pooling Layers:** This can be used to reduce the spatial dimensions of the input image to provide the model with an abstracted form of representation, hence reducing the chance of overfitting.
- **Early stopping:** This consists of consistently monitoring the model’s performance on validation data during the training process and stopping the training whenever the validation error does not improve anymore.
- **Noise injection:** This process consists of adding noise to the inputs or the outputs of hidden layers during the training to make the model more robust and prevent it from a weak generalization.
- **L1 and L2 normalizations:** Both L1 and L2 are used to add a penalty to the loss function based on the size of weights. More specifically, L1 encourages the weights to be spare, leading to better feature selection. On the other hand, L2 (also called weight decay) encourages the weights to be small, preventing them from having too much influence on the predictions.
- **Data augmentation:** This is the process of artificially increasing the size and diversity of the training dataset by applying random transformations like rotation, scaling, flipping, or cropping to the input images.


# Practical Applications of CNNS

- **Image classification:** Convolutional neural networks are used for image categorization, where images are assigned to predefined categories. One use of such a scenario is automatic photo organization in social media platforms.
- **Object detection:** CNNs are able to identify and locate multiple objects within an image. This capability is crucial in multiple scenarios of shelf scanning in retail to identify out-of-stock items.
- **Facial recognition:** this is also one of the main industries of application of CNNs. For instance, this technology can be embedded into security systems for efficient control of access based on facial features.

**Siguiente guia por revisar**
[Python Convolutional Neural Networks (CNN) with TensorFlow Tutorial | DataCamp](https://www.datacamp.com/tutorial/cnn-tensorflow-python)










