

[Restricted Boltzmann Machine (RBM) with Practical Implementation | by Amir Ali | Aorb Tech | Medium](https://medium.com/machine-learning-researcher/boltzmann-machine-c2ce76d94da5)


# The Boltzman Machine
*Boltzmann Machine* was first invented in 1985 by Geoffrey Hinton. _Boltzmann_ ==Machine _is a_ generative unsupervised model, which involves learning a probability distribution from an original dataset and using it to make inferences about never before seen data==

_Boltzmann_ Machine has an input layer (also referred to as the _visible layer_) and one or several hidden layers (also referred to as the _hidden layer_).

<div style="text-align:center">
<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*YTZo3rydalAJmXuDY4B4ug.png" width=500>
</div>


Boltzmann Machine uses neural networks with neurons that are connected (bidirectional) not only to other neurons in other layers but also to neurons within the same layer. _Boltzmann Machine_ ==doesn’t expect input data, it generates data==. ==Neurons generate information regardless they are hidden or visible==.

For _Boltzmann Machine_ all neurons are the same, it doesn’t discriminate between _hidden_ and _visible neurons_. For Boltzmann Machine whole things are system and its generating state of the system.

>[!note] Example
> Suppose for example we have a nuclear power station and there a re certain things we can measure in a nuclear power plant like the temperature of the containment building, ho quickly turbine is spinning, etc.
> 
> The are lots of thing we are not measuring, like the speed of the wind, etc. All this parameters together form a system, they all work together. All these parameters are binary. So we get a whole bunch of binary numbers that tell us something about the state of the power station.
> 
> What we would like to do, is we want to notice that when it is going to in an unusual state. A state that is not like a normal state which we had seen before. And we don’t want to use supervised learning for that. Because we don’t want to have any examples of states that cause it to blow up.
> 
> We would rather be able to detect that when it is going into such a state without even having seen such a state before. And we could do that by building a model of a normal state and noticing that this state is different from the normal states.
> 
> **That what _Boltzmann Machine represents_**


The way this system work, we use our training data and feed into the _Boltzmann Machine as input to help the system adjust its weights._ It learns from the input, what are the possible connections between all these parameters, how do they influence each other and therefore it becomes a machine that represents our system.

_Boltzmann Machine learns how the system works in its normal states through a good example._

>[!tip] Boltzmann Machines
>Boltzmann Machine consists of a neural network with an input layer and one or several hidden layers. The neurons in the neural network make ==stochastic decisions== about whether to turn on or off based on the data we feed during training and the cost function the Boltzmann Machine is trying to minimize.

By doing so, the Boltzmann Machine discovers interesting features about the data, which help model the complex underlying relationships and patterns present in the data.

Training this type of systems (Unrestricted Boltzmann Machines) is very inefficient.

Boltzmann Machines are primarily divided into two categories: **Energy-based Models ([[#An Energy-Base Model|EBMs]])** and **Restricted Boltzmann Machines ([[#Restricted Boltzmann Machine|RBM]])**. When these RBMs are stacked on top of each other, they are known as **Deep Belief Networks (DBN)**.

# An Energy-Base Model
Some deep learning architectures use the idea of energy as a metric fo the measurement of the model's quality.

One purpose of deep learning models is to encode dependencies between variables. The capturing of dependencies happens through associating of scalar energy to each configuration of the variables, which serves as a measure of compatibility. ==High energy means bad compatibility==. ==An energy-based model tries always to minimize a predefined energy function==. The energy function for the RBMs is defined as:

**A joint configuration, ($\textbf{v}$, $\textbf{h}$) of the visible and hidden units has an energy given by:

$$
E(\textbf{v}, \textbf{h}) = - \sum_i \alpha_i \ v_i - \sum_j b_j \ h_j - \sum_{i, j} v_i \ h_j \ w_{i, j}
$$
The training of RBM consists of the finding of parameters for given input values so that the energy reaches a minimum.
# Restricted Boltzmann Machine

What makes RBMs different from Boltzmann machines is that visible node isn’t connected to each other, and hidden nodes aren’t connected with each other.

<div style="text-align:center">
<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*qP7zFsyjb1sCVpV6IBIqOw.png" >
</div>

- RBM is the neural network that belongs to the energy-based model
	
- It is a probabilistic, unsupervised, generative deep machine learning algorithm.
	
- ==RBM’s objective is to find the joint probability distribution that maximizes the log-likelihood function==.
	
- RBM is undirected and has only two layers, Input layer, and hidden layer
	
- All visible nodes are connected to all the hidden nodes. RBM has two layers, visible layer or input layer and hidden layer so it is also called an a**symmetrical bipartite graph.**

==Since RBMs are undirected, they don’t adjust their weights through gradient descent and backpropagation. They adjust their weights through a process called== [contrastive divergence](http://deeplearning.net/tutorial/rbm.html). At the start of this process, weights for the visible nodes are randomly generated and used to generate the hidden nodes. These hidden nodes then use the same weights to reconstruct visible nodes. The weights used to reconstruct the visible nodes are the same throughout. However, the generated nodes are not the same because they aren’t connected to each other.

## How do Restricted Boltzmann Machine Work?

In an RBM, we have a symmetric bipartite graph where no two units within the same group are connected. Multiple RBMs can also be `stacked` and can be fine-tuned through the process of gradient descent and back-propagation. Such a network is called a Deep Belief Network.

RBM is a Stochastic Neural Network which means that each neuron will have some random behavior when activated. ==There are two other layers of bias units (hidden bias and visible bias) in an RBM. This is what makes RBMs different from autoencoders.== The hidden bias RBM produces the activation on the forward pass and the visible bias helps RBM to reconstruct the input during a backward pass. The reconstructed input is always different from the actual input as there are no connections among the visible units and therefore, no way of transferring information among themselves.


<div style="text-align:center">
<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*4JX1ItFmjbNcAlOcokxZJg.png" >
</div>


The above image shows the first step in training an RBM with multiple inputs. 
- The inputs are multiplied by the weights and then added to the bias. 
- The result is then passed through a sigmoid activation function $S(x)$ and the output determines if the hidden state gets activated or not. 
- ==Weights will be a matrix with the number of input nodes as the number of rows and the number of hidden nodes as the number of columns==. 
- The first hidden node will receive the vector multiplication of the inputs multiplied by the first column of weights before the corresponding bias term is added to it

The equation we get in this step would be,

$$
\textbf{h}^{(1)} = S(\textbf{v}^{(0)T} \ W + \textbf{a})
$$

Where $\textbf{h}(1)$ and $\textbf{v}(0)$ are the corresponding vectors (column matrices) for the hidden and the visible layers with the superscript as the iteration $\textbf{v}(0)$ means the input that we provide to the network and $\textbf{a}$ is the hidden layers bias vector.

<div style="text-align:center">
<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*qWa1NOZq1JArIlZgdJ4RkQ.png" >
</div>

Now this image shows the reverse phase or the **reconstruction** phase. It is similar to the first pass but in the opposite direction. The equation comes out to be:

$$
\textbf{v}^{(1)} = S(\textbf{h}^{(1)} \ W^{T} + \textbf{b})
$$

where $\textbf{v}^{(1)}$ and $\textbf{h}^{(1)}$ are the corresponding vectors (column matrices) for the visible and the hidden layers with the superscript as the iteration and **b** is the visible layer bias vector.

### The learning process

Now, the difference $\textbf{v}^{(0)} - \textbf{v}^{(1)}$ can be considered as the reconstruction error that we need to reduce in subsequent steps of the training process. So the weights are adjusted in each iteration so as to minimize this error and this is what the learning process essentially is. Now, let us try to understand this process in mathematical terms without going too deep into mathematics. 

In the forward pass, we are calculating the probability of output $\textbf{h}^{(1)}$ given the input $\textbf{v}^{(0)}$ and the weights $W$ denoted by:

$$
p(\textbf{h}^{(1)} \ | \ \textbf{v}^{(0)} \ ; \ W  )
$$

And in the backward pass, while reconstructing the input, we are calculating the probability of output $\textbf{v}^{(1)}$ given the input $\textbf{h}^{(1)}$ and the weights $W$ denoted by:

$$
p(\textbf{v}^{(1)} \ | \ \textbf{h}^{(1)} \ ; \ W  )
$$
==The weights used in both the forward and the backward pass are the same==. Together, these two conditional probabilities lead us to the joint distribution of inputs and the activations:

$$
p(\textbf{v} \, , \ \textbf{h})
$$
Let us try to see how the algorithm reduces loss or simply put, how it reduces the error at each step. Assume that we have two normal distributions, one from the input data (**denoted by p(x)**) and one from the reconstructed input approximation (**denoted by q(x)**). The difference between these two distributions is our error in the graphical sense and our goal is to minimize it, i.e., bring the graphs as close as possible. This idea is represented by a term called the [Kullback–Leibler divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence).

KL-divergence measures the non-overlapping areas under the two graphs and the RBM’s optimization algorithm tries to minimize this difference by changing the weights so that the reconstruction closely resembles the input. The graphs on the right-hand side show the integration of the difference in the areas of the curves on the left.


<div style="text-align:center">
<img src="https://miro.medium.com/v2/resize:fit:786/format:webp/1*u8iwkCv4Imu98GdsyaXbUw.png" width=500px>
</div>

This gives us intuition about our error term. Now, to see how actually this is done for RBMs, we will have to dive into how the loss is being computed. All common training algorithms for RBMs approximate the log-likelihood gradient given some data and perform gradient ascent on these approximations.


## Contrastive Divergence

Boltzmann Machines (and RBMs) are Energy-based models and a joint configuration, **(v,h)** of the visible and hidden units has energy given by:

$$
E(\textbf{v}, \textbf{h}) = - \sum_{i \ \in \ visible} \alpha_i \ v_i - \sum_{j \ \in \ hidden} b_j \ h_j - \sum_{i, j} v_i \ h_j \ w_{i, j}
$$

$$
E(\textbf{v}, \textbf{h}) = - \textbf{a}^T \textbf{v} \ - \ \textbf{b}^T \textbf{h} \ - \ \textbf{v}^T \textbf{W} \textbf{h}
$$

Where $\textbf{v}_i$, $\textbf{h}_j$ are the binary states of visible unit $i$ and hidden unit $j$, $\alpha_i$, $\textbf{b}_j$ are their biases and $w_{ij}$ is the weight between them.

The network assigns a probability to every posible pair of a visible and hidden vector via this energy function:

$$
p(\textbf{v}, \textbf{h}) = \large \dfrac{1}{Z} {e}^{-E(\textbf{v}, \textbf{h})}
$$

The probability that the network assigns to a visible vector, $v$, is given by summing over all possible hidden vectors:

$$
p(\textbf{v}) = \large \dfrac{1}{Z} \sum_h {e}^{-E(\textbf{v}, \textbf{h})}
$$

**Z** here is the partition function and is given by summing over all possible pairs of visible and hidden vectors:

$$
Z = \large \sum_{\textbf{v}, \textbf{h}} e^{-E(\textbf{v}, \textbf{h})}
$$

This gives us:

$$
p(\textbf{v}) =  \large \dfrac{\sum_h {e}^{-E(\textbf{v}, \textbf{h})}}{\sum_{\textbf{v}, \textbf{h}} e^{-E(\textbf{v}, \textbf{h})}}
$$
The log-likelihood gradient or the derivative of the log probability of a training vector with respect to weight is surprisingly simple:

$$
\dfrac{\partial \ log \ p(\textbf{v})}{\partial w_{i, j}} = \langle \textbf{v}_i \ \textbf{h}_j \rangle_{data} - \langle \textbf{v}_i \ \textbf{h}_j \rangle_{model}
$$


Where the angle brackets are used to denote expectations under the distribution specified by the subscript that follows. This leads to a very simple learning rule for performing stochastic steepest ascent in the log probability of the training data:

$$
\Delta w_{i, j} = \alpha(\langle \textbf{v}_i \ \textbf{h}_j \rangle_{data} - \langle \textbf{v}_i \ \textbf{h}_j \rangle_{model})
$$

where $\alpha$ is a learning rate. The important thing to note here is that because there are no direct connections between hidden units in an RBM, it is very easy to get an unbiased sample of $\langle v_i, h_j\rangle$ data. Getting an unbiased sample of $\langle v_i, h_j\rangle$ model.

However, is much more difficult. This is because it would require us to run a Markov chain until the stationary distribution is reached (which means the energy of the distribution is minimized — equilibrium!) to approximate the second term.

So instead of doing that, we perform [Gibbs Sampling](https://en.wikipedia.org/wiki/Gibbs_sampling) from the distribution. It is a Markov Chain Monte Carlo (**MC**) algorithm for obtaining a sequence of observations which are approximated from a specified multivariate probability distribution when direct sampling is difficult (like in our case). The Gibbs chain is initialized with a training example $\textbf{v(0)}$ of the training set and yields the sample $\textbf{v(k)}$ after **k** steps.

Each step $t$ consists of sampling $\textbf{h(t)}$ from $p(\textbf{h} | \textbf{v(t)})$ and sampling $\textbf{v(t+1)}$ from $p(\textbf{v} | \textbf{h(t)})$ subsequently (the value $k=1$ surprisingly works quite well). 

The learning rule becomes

$$
\Delta w_{i, j} = \alpha(\langle \textbf{v}_i \ \textbf{h}_j \rangle_{data} - \langle \textbf{v}_i \ \textbf{h}_j \rangle_{recon})
$$

The learning works well even though it is only crudely approximating the gradient of the log probability of the training data. The learning rule is much more closely approximating the gradient of another objective function called the **Contrastive Divergence** which is the difference between two Kullback-Liebler divergences.

When we apply this, we get:

$$
\large CD_k(W, \textbf{v}^{(0)}) = -\sum_h p(\textbf{h} | \textbf{v}_k) \dfrac{\partial E(\textbf{v}_k, \textbf{h})}{\partial W} + \sum_h p(\textbf{h} | \textbf{v}_k) \dfrac{\partial E(\textbf{v}_k ,  h)}{\partial W}
$$

Where the second term is obtained after each $k$ steps of Gibbs Sampling.
