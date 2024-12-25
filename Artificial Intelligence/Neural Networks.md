An artificial neural network is a collection of smaller units called neurons, which are computing units modeled on the way the human brain processes information

> [!tip]
> Una red neuronal es un aproximador de funciones

# Back propagation
Neural networks learn through a process called **backpropagation**. Backpropagation uses a set of training data that match known inputs to desired outputs. 
1. First, the inputs are plugged into the network and outputs are determined. 
2. Then, an error function determines how far the given output is from the desired output. 
3. Finally, adjustments are made in order to reduce errors

# Estructura de una red neuronal
A collection of neurons is called a layer, and a layer takes in an input and provides an output. Any neural network will have one input layer and one output layer.


https://www.v7labs.com/blog/neural-networks-activation-functions

# Elementos de una arquitectura de redes neuronales

<div style="text-align: center;">
	<figure>
    <img src="https://cdn.prod.website-files.com/5d7b77b063a9066d83e1209c/60d242974bcba9f8c670e03e_Group%20806.jpg">
    <figcaption></figcaption>
    </figure>
</div>

Podemos ver una red neuronal formada por neuronas interconectadas, cada una caracterizada por su **peso**, **sesgo** y **función de activación**. 

- **Capa de entrada**: recibe la información sin procesar del dominio. No se realiza ningún cálculo en esta capa. Los nodos aquí simplemente pasan la información (características) a la capa oculta.
- **Capa oculta**: realiza todo tipo de cálculos sobre las características ingresadas a través de la capa de entrada y transfiere el resultado a la capa de salida. Las capas ocultas suelen usar la misma función de activación.
- **Capa de salida**: es la capa final de la red que lleva la información aprendida a través de la capa oculta y entrega el valor final como resultado. Usualmente usa una función de activación distinta a la de la capa oculta.


# Funciones de activación
Agregan componentes no lineales a la red neuronal.

> [!info]
> An activation function determines how a node responds to its inputs. The function is run against the sum of the inputs and bias, and then the result is forwarded as an output. Activation functions can take different forms, and choosing them is a critical component to the success of a neural network.

Una función de activación decide si una neurona debe activarse o no, es decir, decidirá si la entrada de la neurona a la red es importante o no en le proceso de predicción mediante operaciones matemáticas más simples.
El trabajo de la función de activación es derivar la salida de una conjunto de valores de entrada enviados a un nodo (o capa).

## Binary step function 
$$
f : \mathbb{R} \to \mathbb{R}
$$
$$
f(x) = 
\begin{aligned}
1 \quad, &\quad x>0 \\
0 \quad, &\quad x<0 \\
\end{aligned}
$$
<div style="text-align: center;">
	<figure>
    <img src="https://cdn.prod.website-files.com/5d7b77b063a9066d83e1209c/60d2449a8f32de661dfd2c8b_pasted%20image%200%20(3).jpg" width=400>
    <figcaption></figcaption>
    </figure>
</div>
- No es apta para el aprendizaje automático actual, ya que no es derivable en 0.


## Funciones sigmoide

### Logística

$$
f(x) = \frac{1}{1 + e^{-x}}
$$
- Se usa comúnmente para modelos donde tenemos que predecir la probabilidad como resultado.
- La función es diferenciable y provee un gradiente suave, es decir, evita saltos en los valores de salida.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\logistic.png">
    <figcaption></figcaption>
    </figure>
</div>


**Desventajas**
- Presenta *desvanecimiento de gradiente*.
- Cuando se hace *back propagation* los ajustes a los pesos y sesgos  de la red se harán con cambios muy pequeños, es decir,  aprenderá lentamente.


### Tangente hiperbólica
$$
f(x) = \frac{e^{-x} - e^x}{e^{-x} + e^x}
$$
<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\tanh.png">
    <figcaption></figcaption>
    </figure>
</div>




**Ventajas**
- Mejor que la función logística.
- Al tener una derivada "mayor" su aprendizaje será "más rápido".
- Como la función esta centrada en cero, podemos mapear fácilmente los valores de salida como fuertemente negativos, neutrales o fuertemente positivos.
- Es común su uso en capas ocultas ya que sus valores se encuentran entre $(-1, 1)$, por tanto, la media de la capa oculta resulta ser aproximadamente 0. Esto ayuda a centrar los datos y facilita el aprendizaje para la siguiente capa.

**Desventajas**
- También presenta el *desvanecimiento de gradiente*.



## ReLU
Significa *Unidad Lineal Rectificada*.
El principal problema es que la función ReLU no activa todas las neuronas al mismo tiempo.
Las neuronas sólo se desactivaran si la salida de la transformación lineal es menor que cero.
$$
f(x) = max\{0, x\}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\ReLU.png">
    <figcaption></figcaption>
    </figure>
</div>

- Al no estar acotada para números positivos, da una gradiente constante y "aprende más rápido".


**Desventajas**
- Al generar cero para todos los valores negativos puede generar las llamadas *neuronas muertas*, es decir, durante el entrenamiento solo devuelven el valor de cero, entorpeciendo así el aprendizaje. Esta desventaja se conoce como *the dying ReLU problem*.


## Leaky ReLu
Es una versión mejorada de ReLU que resuelve el *dying ReLU problem* ya que tiene una pequeña pendiente positiva en el área negativa.
$$
f(x) = max\{ 0.01x, x\}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Artificial Intelligence\imgs\Leaky ReLU.png">
    <figcaption></figcaption>
    </figure>
</div>


**Desventajas**
- Es posible que las predicciones no sean consistentes para valores de entrada negativos.
- El gradiente para valores negativos es un valor pequeño que hace que el aprendizaje de los parámetros del modelo lleve mucho tiempo.



## Parametric ReLU
$$ 
f(x) = 
\begin{aligned}
x \quad, &\quad x>0 \\
ax \quad, &\quad x \leq 0 \\
\end{aligned}
$$

## Otras
- GeLu
- Softplus
- Maxout
- ELU
- Swish
- Mish
## Softmax
La función softmax se define como:
$$ 
\text{softmax}(x_i) = \frac{e^{x_i}}{\sum_{j=1}^{n} e^{x_j}} 
$$ 
donde $x_i$ es el valor en la posición $i$ del vector y $n$ es el número total de elementos en el vector.


# Tipos de redes neuronales

## Perceptron
- Perceptrons are the simplest and oldest types of neural networks. They are single-layered neural networks consisting of input nodes connected directly to an output node. 
- Input layers forward the input values to the next layer, by means of multiplying by a weight and summing the results. Hidden layers receive input from other nodes and forward their output to other nodes. Hidden and output nodes have a property called bias, which is a special type of weight that applies to a node after the other inputs are considered. 
- Finally, an activation function determines how a node responds to its inputs.

## Convolutional Neural Networks (CNNs)
 Convolutional neural networks or CNNs are multilayer neural networks that take inspiration from the animal visual cortex. 
 CNNs are useful in applications such as 
 - image processing
 - video recognition, 
 - natural language processing

 **A convolution is a mathematical operation, where a function is applied to another function and the result is a mixture of the two functions**. Convolutions are good at detecting simple structures in an image, and putting those simple features together to construct more complex features. In a convolutional network, this process occurs over a series of layers, each of which conducts a convolution on the output of the previous layer. CNNs are adept at building complex features from less complex ones

## Recurrent Neural Networks (RNNs)
Recurrent neural networks or RNNs, are recurrent because they perform the same task for every element of a sequence, with prior outputs feeding subsequent stage inputs. 
**In a general neural network, an input is processed through a number of layers and an output is produced with an assumption that the two successive inputs are independent of each other, but that may not hold true in certain scenarios**. For example, when we need to consider the context in which a word has been spoken, in such scenarios, dependence on previous observations has to be considered to produce the output. 
RNNs can make use of information in long sequences, each layer of the network representing the observation at a certain time


# Neural Networks Architectures
[Redes neuronales [A-Z] | Kaggle](https://www.kaggle.com/discussions/general/197078)


![][https://onlinelibrary.wiley.com/cms/asset/2ddcd8f3-5c86-4579-a3b6-316ed3b16e8d/adma202208683-fig-0014-m.jpg]



## Feed Forward Neural Networks (FF or FFNN) and Perceptrons (P)
Are very straight forward, they feed information from the front to the back (input and output, respectively). Neural networks are often described as having layers, where each layer consists of either input hidden or output cells in parallel. The simplest somewhat practical network has two input cells and one output cell, which can be used to model logic gates. One usually trains FFNNs trough **back-propagation**, giving the network paired datasets of "what goes in" and "what we want to have coming out". The error being back-propagated is often some variation of the difference between the input and the output (like **MSE** or just the linear difference). Given that the network has enough hidden neurons, it can theoretically always model the relationship between the input and output. Practically their use is a lot more limited but they are popularly combined with other networks to form new networks.

## Radial Basis Function (RBF)
Are FFNNs with **radial basis functions** as activation functions. 

>[!info]
>La **Función de Base Radial (RBF)** es un tipo de función matemática utilizada en el aprendizaje automático, especialmente en redes neuronales y métodos de interpolación. Se caracteriza por depender únicamente de la distancia entre un punto de entrada y un centro predefinido, es decir, su valor solo depende de $\|x−c\|$, donde $x$ es el punto y ccc es el centro. 


## Hopfield Network (HN)


## Markov Chains (MC or discrete time Markov Chain, DTMC)

## Boltzmann Machines (BM)


## Restricted Boltzmann Machines (RBM)


## Autoencoders (AE)


## Support Vector Machines (SVM)

## Kohonen Networks (KN) or Self Organizing (feature) Map (SOM, SOFM)
Use competitive learning to classify data without supervision. Input is presented to the network, after with the network assesses which of its neurons most closely match that input. These neurons are then adjusted to match the input even better, dragging alone their neighbors in the process. How much the neighbors are moved depends on the distance of the neighbors to the best matching units.