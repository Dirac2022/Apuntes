
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
