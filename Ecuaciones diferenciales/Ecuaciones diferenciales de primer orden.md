
# Ecuación diferencial de primer orden

Es una ecuación de la forma
$$
y′ + P(x)y = Q(x) \tag{1}
$$
el cual es lineal respecto a $y$, donde tenemos que $P(x)$ y $Q(x)$ son funciones de $x$ o constantes.

Además las denominaciones que se dan son:
- Si $Q(x) \neq 0$, entonces es una ecuación diferencial lineal no homogénea.
- Si $Q(x) = 0$, entonces es una ecuación diferencial lineal homogénea.


## Método del factor integrante
La ecuación diferencial lineal (1) se resuelve utilizando

$$
f(x) = e^{\int P(x) dx}
$$

llamado **factor integrante**. Multiplicando la ecuación (1) por el factor integrante:

$$
e^{\int P(x) dx} y' + e^{\int P(x) dx} P(x) y = e^{\int P(x) dx} Q(x)
$$

lo cual es equivalente a la expresión

$$
\frac{d}{dx} \left[ e^{\int P(x) dx} y \right] = e^{\int P(x) dx} Q(x)
$$

cuya solución general es por consiguiente

$$
y e^{\int P(x) dx} = \int e^{\int P(x) dx} Q(x) dx + C
$$
