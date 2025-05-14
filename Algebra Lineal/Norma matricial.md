
# Definición

Es una *norma vectorial* en $K^{m \times n}$, es decir, debe cumplir:
 - $||A||  > 0, \text{si } A \neq 0 \quad y \quad ||A|| = 0  \leftrightarrow A=0$
 - $|| \alpha A || = |\alpha| ||A||  \quad \forall \alpha \in K \wedge A \in K^{m \times n}$
 - $||A + B|| \leq ||A||  + ||B|| \quad \forall A , B \in K^{m \times n}$


# Tipos de norma

## Normal de Frobenius
Esta inducida por el producto interno usual en el espacio de matrices de $m \times n$
$$ ||A||_F = \sqrt{traza((A^{*^{t}})A)} $$
Donde $A^{*^{t}}$ corresponde a la matriz conjugada transpuesta de $A$, o simplemente $A^t$ para matrices de $R^{m \times n}$


## Norma 1:
Máxima suma absoluta de entre las columnas de una matriz
$$||A||_1 = \underbrace{max}_{1 \leq j \leq n} \left ( \sum_{i=1}^{m} |a_{i, j}| \right )$$

## Norma infinito
Máxima suma absoluta de entre las filas de una matriz
$$||A||_{\infty} = \underbrace{max}_{1 \leq i \leq m} \left ( \sum_{j=1}^{n} |a_{i, j}| \right )$$