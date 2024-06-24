`Una red neuronal es un aproximador de funciones`

## Elementos de una arquitectura de redes neuronales

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

# Back propagation

# Funciones de activación
Agregan componentes no lineales a la red neuronal.

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
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\IA\imgs\logistic.png">
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
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\IA\imgs\tanh.png">
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
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\IA\imgs\ReLU.png">
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
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\IA\imgs\Leaky ReLU.png">
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

## GeLU



## Softplus


## Maxout


## ELU


## Swish


## Mish

## Softmax
Se usa para redes de clasificación.
