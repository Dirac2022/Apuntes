
# Teorema del límite central
Sean $\mathcal{X}_1, \mathcal{X}_2, \dots , \mathcal{X}_n$ una sucesión de variables aleatorias independientes con $\mathbb{E}(\mathcal{X}_i) = \mu_i$ y $\mathbb{V}(\mathcal{X}_i) = \sigma_i^2$ , ambos finitos. Sea $Y_n = \mathcal{X}_1 + \mathcal{X}_2 + \dots + \mathcal{X}_n$, bajo ciertas condiciones generales, la variable aleatoria $Z_n$ definida por
$$
\large
Z_n = \dfrac{\underset{i}{\sum} \mathcal{X}_i - \underset{i}{\sum} \mu_i}{\sqrt{\underset{i}{\sum} \sigma^2_i}} \ \ , \quad i = 1, \dots , n
$$
tiene una distribución aproximadamente $\mathcal{N}(0, 1)$, normal estándar, cuando $n$ es grande. Es decir, si la función de distribución de $Z_n$ es $F_n$, se tiene que

$$
\underset{n \to \infty}{lim} F_n(z) = {\huge \Phi}(z)
$$
donde ${\large \Phi}(z)$ es la función de distribución normal acumulada (**cdf**)
$$
\Phi(z) = \mathbb{P}[Z \leq z] = \int_{-\infty}^z \dfrac{1}{\sqrt{2\pi}} \ {\Large e}^{-\dfrac{t^2}{2}} dt
$$
A su vez observamos que la variable aleatoria $Y_n = \underset{i}{\sum} \mathcal{X}_i$ puede aproximada por una variable aleatoria distribuida normalmente, ==cualquiera sea la distribución de los== $\mathcal{X}_i$


---
# Covarianza
Sean $X$ y $Y$ variables aleatorias (discretas) con medias $\mu_X = \mathbb{E}(X)$ , $\mu_Y = \mathbb{E}(Y)$. La covarianza de $X$ y $Y$esta definida como

$$
\begin{align*}
Cov(X, Y) & = \mathbb{E}[(X - \mu_X)(Y - \mu_Y)] \\ \\
& = \sum_{(x, y) \in R_{x \ X\times Y}} (x - \mu_X)(y - \mu_Y) \ p(x, y)
\end{align*}
$$

donde $p$ representa la función de masa de la probabilidad conjunta.


**Propiedades**

- $Cov(X, Y) = \mathbb{E}(XY) - \mu_X \cdot \mu_Y$
- Si $X$ e $Y$ son independientes, entonces $Cov(X, Y)=0$
- Lo contrario es falso: ==covarianza nula no siempre implica independencia==.
- Dados $a, b \in \mathbb{R}$, y siempre que exista se tiene $$ Var(aX \pm bY) = a^2Var(X) + b^2Var(Y) + 2abCov(X, Y)$$
- Si $X$ e $Y$ son ==independientes==, de lo anterior se deduce que ==la varianza es aditiva==.


---
# Correlación

Sean $X$ e $Y$ variables aleatorias con desviación estándar $\sigma_X$ , $\sigma_Y$ respectivamente. El **coeficiente de correlación** de $X$ e $Y$, denotado por $\rho_{xy}$ o $Corr(X, Y)$ se define como 

$$
\rho_{xy} = Corr(X, Y) := \dfrac{Cov(X, Y)}{\sigma_x \ \sigma_Y}
$$
**Propiedades**
- $-1 \leq \rho \leq 1$
	
- $Corr(X, Y) = Corr(Y, X)$
	
- Si $X$ e $Y$ son independientes, la correlación es $0$
	
- Si $Corr(X, Y) = \pm 1$, entonces es posible que exista una dependencia lineal.
	- Si es $1$ es una correlación lineal positiva perfecta.
	- Si es $-1$ es negativa perfecta.
	
- Dada $Y = aX + b$
	- Si $a > 0$ , la correlación es 1
	- Si $a<0$ , la correlación es -1
	
- Si $a, b, c$ y $d$ son constantes con $a>0$ y $b>0$, entonces $$ Corr(aX+c, bY+d) = Corr(X, Y) $$
---
