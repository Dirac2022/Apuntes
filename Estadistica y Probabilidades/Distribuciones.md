
# Distribuciones discretas

## Distribución binomial

Hay problemas donde un experimento consiste de $n$ ensayos (o sub experimentos) de Bernoulli $\varepsilon_1,\varepsilon_2, \dots, \varepsilon_n \,$. Una secuencia de $n$ ensayos de Bernoulli  forman un **proceso de Bernoulli** o **experimento binomial** si:

- Cada ensayo solo tiene dos resultados posibles: **Éxito $E$** o **Fracaso $F$**.
- ==Los ensayos son independientes==.
- La probabilidad de éxito $p$ permanece constante de ensayo a ensayo.

El espacio muestral de los $n$ ensayos tiene $2^n$ elementos o sucesos los cuales son una sucesión de $n$ símbolos $E$ y $F$.

$$
\Omega = {\omega_ = (\omega_1, \omega_2, \dots, \omega_n) : \omega_i = E \ \lor F }
$$
es decir $\Omega = \{ EEFEFEF \dots EFE, \dots  \}$

Se define a la variable aleatoria $X$ como $X(\omega) =$ número de éxitos obtenidos en los $n$ ensayos de Bernoulli. $R_X = \{0,1,\dots, n\} \,$.

$$
\begin{array}{}
\mathcal{X} &  : &  \Omega & \to & \mathbb{R} \\
& & \omega & \to & \mathcal{X}_{(\omega)} = \text{N° de éxitos}
\end{array}
$$

La distribución de probabilidad de la variable aleatoria binomial $X$ se denomina **distribución binomial**, $\mathcal{X} \sim B_i \ (n, p)$ y se denota por $\mathbb{P}[\mathcal{X}=x \ | \ B \, ; \ n, p]$ o $b(\mathcal{X} \, ; \ n, p)$ y se lee como la probabilidad de obtener $x$ éxitos y $n-x$ fracasos.

**Función de masa**

$$
\large
p(x) = 
\begin{cases}
\displaystyle \binom{n}{x} p^x (1-p)^{n-x},  & \text{para } x = 0, 1, \dots, n  \\ \\
0 & \text{ en otros casos}
\end{cases}
$$

**Función de distribución acumulada**

$$
F(x) = \mathbb{P}[\mathcal{X} \leq x ] = \mathbb{P}[\mathcal{X} \leq x | \ B \, ; \ n, p] = 
\begin{cases}
0 & x < 0 \\ \\
\large 
\sum_{k=0}^{\|x\|} \displaystyle \binom{n}{x} p^x (1-p)^{n-x} &  0 \leq x \leq n \\ \\
1 & x \geq n
\end{cases}
$$


**Media o esperanza**

$$
\mu = \mathbb{E}(X) = np
$$

**Varianza**
$$
\sigma_X^2 = Var(X) = np(1-p)
$$





## Distribución de Poisson

Los eventos discretos que se generan en un intervalo continuo (unidad de medida: longitud, área, volumen, tiempo, etc.) forman un proceso de **Poisson** con promedio $\lambda$ si tiene las siguientes propiedades:

1. El número promedio de ocurrencias de eventos en una unidad de medida es conocido e igual a $\lambda$.
2. La ocurrencia de los eventos en unidades de medida contiguas son **independientes**.
3. Sa una unidad de medida suficientemente pequeña $h$, luego:
	1. La probabilidad de éxito en esta unidad pequeña es proporcional a la longitud del intervalo, esto es $\lambda h$.
	2. La probabilidad de la ocurrencia de 2 o más éxitos en esta unidad pequeña es aproximadamente 0.

En un proceso de Poisson de parámetro $\lambda$ se observa $t$ unidades de medida. Definimos $\mathcal{X}$ como

$$
\mathcal{X}(\omega) = \text{número de ocurrencia de eventos en } t \text{ unidades de medida}
$$
- $R_{\mathcal{X}} = {0, 1, 2, \dots}$
- $\mathcal{X} \sim \mathbb{P}(\lambda)$


La variable aleatoria así definida es una **variable aleatoria de Poisson** y la distribución de probabilidad de $\mathcal{X}$, **distribución de Poisson** $N \sim \mathbb{P} (\lambda)$

$$
p(x) = \mathbb{P}[\mathcal{X}=x | P: \lambda t] = {\large e^{-\lambda t}} \dfrac{(\lambda t)^x}{x!} \ \ , \quad x = 0, 1, \dots
$$

- $\lambda t$: número de ocurrencias de los eventos en las $t$ unidades de medida.
- $N$: número de eventos independientes de Poisson que ocurren en un intervalo de tiemnpo $I$.

**Función de distribución** de $\mathcal{X}$

$$
F(x) = \mathbb{P}[\mathcal{X}=x | P: \lambda t] = 
\begin{cases}
0 & , \quad x < 0 \\ \\
{\large \overset{\lfloor x \rfloor}{\underset{k=0}{\sum}}} {\large e}^{-\lambda t} \dfrac{(\lambda t)^k}{k!} & , \quad x \geq 0
\end{cases}
$$

**Media**
$$
\mathbb{E}(X) = \lambda t
$$

**Varianza**
$$
\mathbb{V}(X) = \lambda t
$$


<div style="text-align:center">
<img src="https://upload.wikimedia.org/wikipedia/commons/c/c1/Poisson_distribution_PMF.png" width=400>
</div>




# Distribuciones continuas

## Distribución uniforme

Una variable aleatoria continua $\mathcal{X} \sim U \ (\alpha, \beta)$ se dice **uniformemente distribuida** sobre el intervalo $[\alpha, \beta]$ con $\alpha < \beta$ si la función de densidad de probabilidad (**pdf**) es dada por

$$
f(x)=
\begin{cases}
\dfrac{1}{\beta - \alpha} & , \quad x \in [\alpha, \beta] \\ \\
0 & , \quad \text{otros casos}
\end{cases}
$$

Su función de distribución acumulada:

$$
F(x) = 
\begin{cases}
0 & , \quad x < \alpha \\ \\
\dfrac{x-\alpha}{\beta - \alpha} & , \quad x \in [\alpha, \beta] \\ \\
1 & , \quad x \geq \beta
\end{cases}
$$


**Media**
$$
\mathbb{E}(X) = \dfrac{\alpha + \beta}{2}
$$

**Varianza**
$$
Var(X) = \dfrac{(\beta - \alpha)^2}{12}
$$



## Distribución exponencial

Sea $\mathcal{X}$ una variable aleatoria continua. Se dice que $\mathcal{X}$ tiene distribución exponencial con parámetro real $\lambda$ si su función de densidad (**pdf**) esta dado por

$$
f(x) = 
\begin{cases}
\lambda e^{-\lambda x} & , \quad x \geq 0 \\ \\
0 & ,  \quad \text{otros casos}
\end{cases}
$$

donde $\lambda \in \mathbb{R}$, $\lambda > 0$

La función de distribución de la variable aleatoria $\mathcal{X}$ con distribución exponencial es

$$
F(x) = 
\begin{cases}
0 & , \quad x < 0 \\ \\
1-e^{-\lambda x} &, \quad x \geq 0
\end{cases}
$$

Tambien se le puede presentar en función de $\beta$, donde $\beta = 1/\lambda$ es el periodo promedio en la ocurrencia de un evento de Poisson.

**Media**
$$
\dfrac{1}{\lambda} = \beta
$$
**Varianza**
$$
\dfrac{1}{\lambda^2} = \beta^2
$$



### Relación entre la distribución exponencial y Poisson

Las dos distribuciones se pueden utilizar para descubrir el mismo fenómeno, la distribución de Poisson $N \sim P(\lambda)$ describe el número de ocurrencias de eventos por unidad de medida y la distribución exponencial $\mathcal{X} \sim Exp(\lambda)$, describe el valor de la medida entre ocurrencias sucesivas de eventos.

Sea $\mathcal{X}(\omega)$: número de ocurrencias de un evento en un periodo $t$, definimos $\lambda$ como el número esperado de ocurrencias por unidad de tiempo. Entonces el número esperado de ocurrencias en el intervalo $t$ sea $(\lambda t)$ y la distribución de $\mathcal{X}$ es

$$
\large
\mathbb{P}[X=x] = \dfrac{(\lambda t)^x e^{-\lambda t}}{x!} \ \ ,  \quad x = 0, 1, \dots
$$

Sea $T(t)$: intervalo de tiempo entre ocurrencias sucesivas de eventos

$R_T = \{t \in \mathbb{R} / t > 0\}$. La distribución de $T$ (exponencial) se deduce de la distribución de Poisson.

La probabilidad de la **no ocurrencia de eventos** en el periodo $t$ es $\mathbb{P}[X=0]=e^{-\lambda t}$, y la probabilidad de la **no ocurrencia de eventos** en el intervalo $t$ es igual a que $T$ exceda a $t$, $T > t$. $\mathbb{P}[T > t] = \mathbb{P}[X = 0] = e^{-\lambda t}$, entonces

$$
\mathbb{P}[T \leq t] = 1 - \mathbb{P}[T > t] = 1 - e^{-\lambda t}
$$

**Función de distribución**

$$
F(x) = 
\begin{cases}
0 & , \quad t < 0 \\ \\
1-e^{-\lambda t} &, \quad t \geq 0
\end{cases}
$$

**Distribución exponencial**

$$
f(x) = 
\begin{cases}
\lambda e^{-\lambda t} & , \quad t \geq 0 \\ \\
0 & ,  \quad \text{otros casos}
\end{cases}
$$

### Propiedad de pérdida de memoria

Nos dice que cada instante es como el comienzo de un nuevo periodo aleatorio, que tiene la misma distribución independientemente de cuánto tiempo haya transcurrido, es decir, las probabilidades no se verán influenciadas por la historia del proceso.

La distribución exponencial es la única variable aleatoria continua con la propiedad de **pérdida de memoria**. Esta propiedad nos dice que el tiempo que se debe esperar hasta el próximo evento es siempre $1/\lambda$, sin importar cuánto tiempo se haya esperado para que ocurra una nueva llegada.

Sea $\mathcal{X} \sim Exp(\lambda)$
$$
\mathbb{P} [X > s + t | X > t] = \mathbb{P} [X > s]
$$




## Distribución Normal


Una variable aleatoria continua $\mathcal{X}$ se dice que esta distribuida normalmente con media $\mu \in \mathbb{R}$ y varianza $\sigma^2 > 0$, $\mathcal{X} \sim N(\mu, \sigma^2)$, si su función de densidad de probabilidad (**pdf**) esta dada por

$$
f_{(\mu, \sigma^2)}(x) = \dfrac{1}{\sigma \sqrt{2\pi}} \ {\Large e}^{-\dfrac{1}{2}\left(\dfrac{x-\mu}{\sigma}\right)^2}
$$

Los dos parámetros que determinan completamente la distribución normal son su **media** y su **varianza**.

### Distribución normal estándar

Sea $Z$ una variable aleatoria con distribución normal con media $\mu=0$ y varianza $\sigma^2=1$, entonces $Z$ se llama variable aleatoria normal estándar, su función de densidad es
$$
f(z) = \dfrac{1}{\sqrt{2\pi}} {\Large e}^{-\dfrac{z^2}{2}} \ \ , \ \ \ z \in \mathbb{R}
$$
La función de distribución de $Z$, de denota por $\Phi(z)$, $\mathcal{N}_z(z)$, y esta dado por
$$
\Phi(z) = \mathbb{P}[Z \leq z] = \int_{-\infty}^z \dfrac{1}{\sqrt{2\pi}} \ {\Large e}^{-\dfrac{t^2}{2}} dt
$$

Cualquier variable aleatoria $\mathcal{X}$ normal con media $\mu$ y varianza $\sigma^2$  puede ser transformado a una variable aleatoria estandarizada $Z$, por la siguiente transformación
$$
Z = \dfrac{\mathcal{X} - \mu}{\sigma}
$$

