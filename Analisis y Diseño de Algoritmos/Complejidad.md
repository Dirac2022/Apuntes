
# Big $\mathcal{O}$

Sean $f, g : N \rightarrow \mathbb{R}^+ \cup {0}$. El conjunto de las funciones del orden de $g(n)$, denotado $\mathcal{O}(g(n))$, se define como sigue:
$$\mathcal{O}{(g(n))} =  \{ f(n) : \exists c \in \mathbb{R}^+ , \: \exists x_0 \in \mathbb{N}, \: \forall n \geq x_0, \: f(n) \leq c \cdot g(n) \} $$
diremos que una función $f$ es del orden $g(n)$ cuando $f \in \mathcal{O}{(g(n))}$.

<div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/39/CotaSuperiorAsintotica.png">
</div>



# Big $\Omega$

Sean $f, g : \mathbb{N} \rightarrow \mathbb{R}^+ \cup {0}$. El conjunto $\Omega(g(n))$, se lee omega de $g(n)$, se define como sigue:

$$\Omega{(g(n))} =  \{ f(n) : \exists c \in \mathbb{R}^+ , \: \exists x_0 \in \mathbb{N}, \: \forall n \geq x_0, \: f(n) \geq c \cdot g(n) \} $$

<div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/CotaInferiorAsintotica.png">
</div>


# Big $\Theta$
El conjunto de funciones $\Theta(g(n))$, se lee orden exacto de $g(n)$, se define como

$$\Theta(g(n)) = \mathcal{O}{g(n)} \, \cap \, \Omega(g(n)) $$
es decir, 
$$\Theta{(g(n))} =  \{ f(n) : \exists c_1, c_2 \in \mathbb{R}^+ , \: \exists x_0 \in \mathbb{N}, \: \forall n \geq x_0, \: [c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n) ]\}$$ <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/80/CotaAjustadaAsintotica.png/366px-CotaAjustadaAsintotica.png">
</div>

# Propiedades
Sean las funciones $f, g : \mathbb{N} \rightarrow \mathbb{R}^+ \, \cup \, {0}$ se cumple lo siguiente:

1. $f(n) \in \mathcal{O}{(f(n))}$
2. $f(n) \in \mathcal{O}{(g(n))} \rightarrow \mathcal{O}{(f(n))} \subset \mathcal{O}{(g(n))}$
3. $\mathcal{O}{(f(n))} = \mathcal{O}{(g(n))} \leftrightarrow [ f(n) \in \mathcal{O}{(g(n))} \wedge g(n) \in \mathcal{O}{(f(n)) ]}$


# Propiedades
Sean las funciones $f, g : \mathbb{N} \rightarrow \mathbb{R}^+ \,  \cup \, {0}$.

1. $$\lim_{n \to \infty} \dfrac{f(n)}{g(n)} = 0 \to \mathcal{O}{(f(n))} \subset \mathcal{O}{(g(n))} ,\quad f(n) \: \text{es mejor que} \: g(n)$$
2. $$\lim_{n \to \infty} \dfrac{f(n)}{g(n)} = k \neq 0 \to \mathcal{O}{(f(n))} = \mathcal{O}{(g(n))} ,\quad \text{cualquiera}$$
3. $$ \lim_{n \to \infty} \dfrac{f(n)}{g(n)} = \infty \to \mathcal{O}{(g(n))} \subset \mathcal{O}{(f(n))} ,\quad g(n) \: \text{es mejor que} \: f(n)$$



# o-notation
La cota superior asintótica proporcionada por la notación $\mathcal{O}$ puede o no ser asintóticamente ajustada. La cota $2n^2= \mathcal{O}{(n^2)}$ es asintóticamente ajustada, pero la cota $2n= \mathcal{O}{(n^2)}$ no lo es. Utilizamos la notación $o$ para denotar una cota superior que **no es asintóticamente ajustada**. Se define $o(g(n))$  ("little-oh of $g$ of $n$") como el conjunto

$$ o(g(n)) = \{ f(n) : \forall c > 0, \exists n_0 > 0 \: \text{tal que} \: 0 \leq f(n) < c \cdot g(n) , \: \forall n \geq n_0 \}$$

Por ejemplo,  $2n = o(n^2)$, pero $2n^2 \neq o(n^2)$

 