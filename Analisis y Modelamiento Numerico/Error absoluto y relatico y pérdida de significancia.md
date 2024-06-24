Cuando un número real $X$ es aproximado por otro $\hat{x}$, el error es $x-\hat{x}$.
- El **error absoluto es** $$|x - \hat{x}|$$
- el **error relativo es** $$|\frac{x - \hat{x}}{x}|$$ 
**Error relativo en la representación de un número $x$ por un número en punto flotante cercano**
 $$|\frac{x - fl(x)}{x}| \leq \varepsilon $$

# Loss of Precision

## Teorema de la perdida de precision
Si $x$ y $y$ son números de maquina binarios en punto flotante normalizados positivos tal que $x > y$ y 
$$ 2^{-q} \leq 1 - \frac{y}{x} \leq 2^{-p}$$

entonces a lo más $q$ y al menos $p$ bits binarios significativos se pierden en la substracción $x-y$
