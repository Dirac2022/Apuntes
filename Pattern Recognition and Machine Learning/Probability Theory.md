
# Rules of Probability

## Sum Rule
$$ p(X) = \sum_{Y} p (X, Y) $$
## Product Rule
$$ p(X,Y) = p(Y|X)p(X) $$
Donde $p(X,Y)$ es una **probabilidad conjunta** y se lee como la *probabilidad de X y Y*. De forma similar, la cantidad $p(Y|X)$ es la **probabilidad condicionada** y se lee como *la probabilidad de Y dado X*, mientras que $p(X)$ es la **probabilidad marginal** y es simplemente la *probabilidad de X*.
$$   p(X,Y) = p(Y, X) $$
$$   p(X,Y) = p(Y|X)p(X)  = p(X|Y)p(Y) = p(Y, X) $$
Vemos que de la [[#Product Rule|regla del producto]] y la simetría de la probabilidad conjunta se obtiene la siguiente relación
## Bayes' theorem
$$ p(Y|X) = \frac{p(X|Y)p(Y)}{p(X)} $$

Usando la [[#Sum Rule|regla de la suma]] el denominador en el teorema de Bayes puede ser expresado en términos de cantidades que aparecen en el numerador
$$ p(X) = \sum_{Y} p(X|Y)p(Y) $$

## Independence
Si la distribución de dos variables se factoriza en el producto de los marginales tal que
$$ p(X,Y) = p(X)p(Y) $$
entonces $X$ y $Y$ se dice que son **independientes**.
De la regla del producto, vemos que 
$$ p(X|Y) = p(Y) $$
y, entonces la *distribución condicional* de $Y$ dado $X$ es de hecho *independiente* del valor de $X$.

# Probability densities
	