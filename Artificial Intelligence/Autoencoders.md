Implementación: [Introduction to Autoencoders [Theory and Implementation] | by Sunny Bhaveen Chandra | Medium](https://medium.com/@c17hawke/introduction-to-autoencoders-theory-and-implementation-72fed7cf2f70)


> [!tip]  What are autoencoders?
> An autoencoder is a neural network that is trained to reconstruct its input. It consist of two parts: and encoder and a decoder. The encoder takes the input and compresses it into a lower-dimensional representation, while the decoder takes this compressed representation and reconstructs the original input.
>
> The goal of the autoencoder is to minimize the difference between the input and the reconstructed output. 

<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*DBrvoyVyG0Z-P4VjJdrw_g@2x.png" >


# Autoencoders
[Autoencoders. What is an autoencoder? | by Learn AI | Medium](https://medium.com/@divakar1591/autoencoders-6fab1a9a9f9c)

The autoencoder is a complicated mathematical model that trains on **unlabeled** and **unclassified data** and is used to map the input data to another compressed feature representation before reconstructing the input data from that feature representation.

The aim of an autoencoder is to learn a lower-dimensional representation (encoding) for a higher-dimensional data, by training the network to capture the most important parts of the input data 

<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/0*zwgXca2_yxX-9EJA.png" >

## The architecture of autoencoders

Autoencoders consist of three parts:

1. **Encoder**: A module that compresses the train-validate-test set input data into an encoded representation that is typically several orders of magnitud smaller than the input data.
	
2. **Bottleneck**: A module that contains the compressed knowledge representations and is therefore the most important part of the network.
	
3. **Decoder**: A module that helps the network *decompress* the knowledge representations and reconstructs the data back from its encoded form. The output is then compared with a ground truth.


<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/0*WcbbJVDpglh3PUke.png" >


## The relationship between the encoder, bottleneck and decoder

Autoencoders are made up of four major components:

- **Encoder**: The model learns how to compress the input data into an encoded form by reducing the input dimensions
	
- The layer that includes the compressed representation of the input data is known as the **bottleneck**. This is the smallest input data dimension imaginable.
	
- **Decoder**: When a model learns how to reconstruct data from an encoded representation as close as feasible to the original input, it is called a decoder.
	
- **Reconstruction Loss**: This is a method for determining how well a decoder works and how close the output is to the original input.


## How to train autoencoders?

You need to set 4 hyperparameters before _training_ an autoencoder:

- **Code size**: It represents the number of nodes in the middle layer. Smaller size results in more compression.
- **Number of layers**: The autoencoder can consist of as many layers as we want.
- **Number of nodes per layer**: The number of nodes per layer decreases with each subsequent layer of the encoder, and increases back in the decoder. ==The decoder is symmetric to the encoder in terms of the layer structure==.
- **Loss function:** We either use mean squared error or binary cross-entropy. If the input values are in the range $[0, 1]$ then we typically use cross-entropy, otherwise, we use the mean squared error.

## Types of autoencoders

Five popular autoencoders:

1. Undercomplete autoencoders
2. Sparse autoencoders
3. Contractive autoencoders
4. Denoising autoencoders
5. Variational Autoencoders (for generative modeling)


### Undercomplete Autoencoders


When we think of dimensionality reduction, we tend to think in methods like [[PCA]]. However, [[PCA]] can only build linear relationships. Undercomplete autoencoders can learn non-linear relationships and, therefore, perform better in dimensionality reduction.

This form of nonlinear dimensionality reduction where the autoencoder learns a non-linear manifold is also termed as _manifold learning_.

Although the reconstruction loss can be anything depending on the input and output, we will use an L1 loss to depict the term (also called the _norm loss_) represented by:

$$
L = |x - \hat{x}|
$$
Where $\hat{x}$ represents the predicted output and $x$ represents the ground truth.
