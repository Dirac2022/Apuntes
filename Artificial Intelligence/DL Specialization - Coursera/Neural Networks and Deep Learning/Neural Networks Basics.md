# Binary Classification


## Notation

- $(x, y)$     $x \in \mathbb{R}^{n_x}$ ,  $y \in \{0, 1\}$ 
- $m$ training examples: $\{(x^{(1)}, y^{(1)})\ , \ \ (x^{(2)}, y^{(2)})\ , \ \ \dots\ , \ \ (x^{(m)}, y^{(m)})\}$
- $X$ matrix of examples
	- ==Columns are each training example, instead of rows==. With this approach makes the implementations in a neural network much easier.
	- $X \in \mathbb{R}^{n_x, m}$
	- `X.shape = (nx, m)`
- $Y = [y^{(1)} \ , \ \  y^{(2)} \ , \dots , y^{(m)}]$
	- $Y \in \mathbb{R}^{1 \times m}$
	- `Y.shape = (1, m)`


# Broadcasting in Python

**General principle**

$$
\underset{\text{matrix}}{(m, n)} \quad +,\ -,\ *,\ /  \quad (1, n) \to (m, n) , \quad (m, 1) \to (m, n)
$$

