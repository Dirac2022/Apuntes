
# Teorema de Gershgorin

## Teorema

El espectro de una matriz  $A_{n \times n}$ (es decir, el conjunto de sus valores propios) está contenido en la unión de los siguientes $n$ discos, $D_i$, en el plano complejo:

$$
D_i = \left\{ z \in \mathbb{C} : |z - a_{ii}| \leq \sum_{\substack{j=1 \\ j \neq i}}^{n} |a_{ij}| \right\} \quad (1 \leq i \leq n)
$$

### Demostración
Sea $\lambda$ cualquier elemento del espectro de $A$. Seleccione un vector $x$ tal que $Ax = \lambda x$ y $\|x\|_\infty = 1$. Sea $i$ un índice para el cual $|x_i| = 1$. Dado que $(Ax)_i = \lambda x_i$, tenemos

$$
\lambda x_i = \sum_{j=1}^{n} a_{ij} x_j
$$

Por lo tanto,

$$
(\lambda - a_{ii}) x_i = \sum_{\substack{j=1 \\ j \neq i}}^{n} a_{ij} x_j
$$

Tomando valores absolutos y usando la desigualdad triangular y $|x_j| \leq 1 = |x_i|$, tenemos

$$
|\lambda - a_{ii}| \leq \sum_{\substack{j=1 \\ j \neq i}}^{n} |a_{ij}| |x_j| \leq \sum_{\substack{j=1 \\ j \neq i}}^{n} |a_{ij}|
$$

Por lo tanto, $\lambda \in D_i$.

## Teorema sobre los discos de valores propios
Si la matriz $A$ se diagonaliza mediante la transformación de similitud $P^{-1}AP$, y si $B$ es cualquier matriz, entonces los valores propios de $A + B$ se encuentran en la unión de los discos

$$
\{ \lambda \in \mathbb{C} : |\lambda - \lambda_i| \leq \kappa_{\infty}(P) \|B\|_{\infty} \}
$$

donde $\lambda_1, \lambda_2, \ldots, \lambda_n$ son los valores propios de $A$, y $\kappa_{\infty}(P)$ es el [[Condicionamiento#Numero de condición de una matriz $ kappa$(A)|número de condición]]  de $P$.

### Demostración
Podemos establecer un resultado algo más preciso. Si $P^{-1}AP = D$, la diagonal de la matriz diagonal $D$ consiste en $\lambda_1, \lambda_2, \ldots, \lambda_n$. Usando "sp" para espectro, tenemos

$$
\text{sp}(A + B) = \text{sp}(P^{-1}(A + B)P) = \text{sp}(D + P^{-1}BP)
$$

Aplicando el Teorema de Gershgorin a $D + C$, con $C = P^{-1}BP$, concluimos que el espectro de $A + B$ está en la unión de los discos de Gershgorin de $D + C$, que son

$$
\left\{ \lambda \in \mathbb{C} : |\lambda - \lambda_i - c_{ii}| \leq \sum_{\substack{j=1 \\ j \neq i}}^{n} |d_{ij} + c_{ij}| = \sum_{\substack{j=1 \\ j \neq i}}^{n} |c_{ij}| \right\}
$$

Por la desigualdad triangular y la definición de $\|C\|_{\infty}$, tenemos

$$
|\lambda - \lambda_i| \leq |\lambda - \lambda_i - c_{ii}| + |c_{ii}| \leq |c_{ii}| + \sum_{\substack{j=1 \\ j \neq i}}^{n} |c_{ij}|
$$

$$
\leq \|C\|_{\infty} \leq \|P^{-1}\|_{\infty} \|B\|_{\infty} \|P\|_{\infty} = \kappa_{\infty}(P) \|B\|_{\infty}
$$

El Teorema sobre los discos indica que cuando una matriz $A$ es perturbada, sus valores propios se verán perturbados por una cantidad que no excede $\kappa_{\infty}(P) \|B\|_{\infty}$, donde $B$ es la matriz perturbadora y $\kappa_{\infty}(P)$ es el número de condición de $P$ calculado a partir de la norma $\ell_{\infty}$ de la matriz. 


# Método de la potencia

## Autovalor dominante
Sea $A \in \mathbb{C}^{n \times n}$ una matriz con autovalores $\lambda_1, \lambda_2, \dots, \lambda_n$. $\lambda_1$ es llamado **autovalor dominante** de $A$ si
$$
|\lambda_1| > |\lambda_i|,  \quad \quad i = 2, \dots ,  n
$$
Los autovectores correspondientes a $\lambda_i$ son llamados **autovectores dominantes** de $A$.

## Método de la potencia
Este procedimiento está diseñado para computar el valor propio dominante y un vector propio correspondiente al valor propio dominante. Para que la teoría proceda sin problemas, es necesario asumir que $A$ tiene las siguientes dos propiedades:

1. Hay un único valor propio de módulo máximo (autovalor dominante).
2. Existe un conjunto linealmente independiente de $n$ vectores propios.

De acuerdo con la segunda suposición, existe una base $\{u^{(1)}, u^{(2)}, \ldots, u^{(n)}\}$ para $\mathbb{C}^n$ tal que

$$
A u^{(j)} = \lambda_j u^{(j)} \quad (1 \leq j \leq n) \tag{1}
$$

Sea $x^{(0)}$ cualquier elemento de $\mathbb{C}^n$ tal que cuando $x^{(0)}$ se expresa como una combinación lineal de los elementos base $u^{(1)}, u^{(2)}, \ldots, u^{(n)}$, el coeficiente de $u^{(1)}$ no es cero. Por lo tanto,

$$
x^{(0)} = a_1 u^{(1)} + a_2 u^{(2)} + \cdots + a_n u^{(n)} \quad (a_1 \neq 0) \tag{2}
$$

Formamos entonces

$$
x^{(1)} = A x^{(0)}, \quad x^{(2)} = A x^{(1)}, \quad \ldots, \quad x^{(k)} = A x^{(k-1)}
$$

de modo que

$$
x^{(k)} = A^k x^{(0)} \tag{3}
$$

En el análisis que sigue, no hay pérdida de generalidad al absorber todos los coeficientes $a_j$ en los vectores $u^{(j)}$ que multiplican. Por lo tanto, podemos escribir la Ecuación (2) como

$$
x^{(0)} = u^{(1)} + u^{(2)} + \cdots + u^{(n)}
$$

Mediante esta ecuación y (3), tenemos

$$
x^{(k)} = A^k u^{(1)} + A^k u^{(2)} + \cdots + A^k u^{(n)}
$$

Usando la Ecuación (1), llegamos a

$$
x^{(k)} = \lambda_1^k u^{(1)} + \lambda_2^k u^{(2)} + \cdots + \lambda_n^k u^{(n)}
$$

Esta última ecuación puede reescribirse en la forma

$$
x^{(k)} = \lambda_1^k \left[ u^{(1)} + \left( \frac{\lambda_2}{\lambda_1} \right)^k u^{(2)} + \cdots + \left( \frac{\lambda_n}{\lambda_1} \right)^k u^{(n)} \right]
$$

Dado que $|\lambda_1| > |\lambda_j|$ para $2 \leq j \leq n$, vemos que los coeficientes $\left( \frac{\lambda_j}{\lambda_1} \right)^k$ tienden a 0 y el vector dentro de los corchetes converge a $u^{(1)}$ conforme $k \to \infty$. 

Para simplificar la notación, escribimos $x^{(k)}$ en la forma

$$
x^{(k)} = \lambda_1^k \left[ u^{(1)} + \epsilon^{(k)} \right]
$$

donde $\epsilon^{(k)} \to 0$ conforme $k \to \infty$. Para poder tomar razones, sea $\varphi$ cualquier funcional lineal sobre $\mathbb{C}^n$ para el cual $\varphi(u^{(1)}) \neq 0$. Recordemos que un funcional lineal $\varphi$ satisface $\varphi(\alpha x + \beta y) = \alpha \varphi(x) + \beta \varphi(y)$, para escalares $\alpha$ y $\beta$ y vectores $x$ y $y$. (Por ejemplo, $\varphi$ podría simplemente evaluar el $j$-ésimo componente de cualquier vector dado.) Entonces

$$
\varphi(x^{(k)}) = \lambda_1^k \left[ \varphi(u^{(1)}) + \varphi(\epsilon^{(k)}) \right] \tag{4}
$$

En consecuencia, las siguientes razones convergen a $\lambda_1$ conforme $k \to \infty$:

$$
r_k \equiv \frac{\varphi(x^{(k+1)})}{\varphi(x^{(k)})} = \lambda_1 \left[ \frac{\varphi(u^{(1)}) + \varphi(\epsilon^{(k+1)})}{\varphi(u^{(1)}) + \varphi(\epsilon^{(k)})} \right] \to \lambda_1
$$

Esto constituye el método de la potencia para computar $\lambda_1$. Dado que la dirección del vector $x^{(k)}$ se alinea más y más con $u^{(1)}$ conforme $k \to \infty$, el método también puede darnos el vector propio $u^{(1)}$. 

## Observación
En las realización de un algoritmo para el método de la potencia, **es recomendable introducir una normalización de los vectores $x^{(k)}$** ya que de otra manera podrían converger a cero o crecer sin límite.

## Teorema (cociente de Rayleigh)
Si $x$ es un autovector de una matriz $A$, entonces su correspondiente autovalor es dado por 
$$
\lambda = \frac{\langle Ax, x\rangle}{\langle x ,x \rangle}
$$
La demostración sale de $Ax = \lambda x$ aplicando producto interno a $\langle Ax, x\rangle$.


## Método de la potencia con desplazamiento
En algunos casos, la convergencia puede ser mejorada significativamente usando un
desplazamiento adecuado. Por tanto, si $\sigma$ es un desplazamiento adecuado tal que $\lambda _1 − \sigma$ es el autovalor dominante de $A − \sigma I$ y si aplicamos el método de la potencia a la matriz $A − \sigma I$, entonces la tasa de convergencia es determinada por la razón:
$$
\left|\frac{\lambda_2 - \sigma}{\lambda_1 - \sigma} \right|
$$
en vez de
$$
\left| \frac{\lambda_2}{\lambda_1} \right|
$$
Esto se debe a que el desplazamiento de la matriz $A$ por $\sigma$ conlleva a que los autovalores de $A$ sean desplazados por $\sigma$, pero los autovectores no se alteran. [[Valores y vectores propios#Teorema sobre los valores propios de $p(A)$|Revisar teorema]]



## Teorema
Si $\lambda$ es un valor propio de $A$, y $A$ es no singular, entonces $\lambda^{-1}$ es un valor propio de $A^{-1}$.
## Método de la potencia inversa

El teorema anterior sugiere un mecanismo para calcular el valor propio más pequeño de $A$. Supongamos que los valores propios de $A$ pueden ordenarse de la siguiente manera:

$$
|\lambda_1| \geq |\lambda_2| \geq \cdots \geq |\lambda_{n-1}| > |\lambda_n| > 0
$$

Esta hipótesis implica que $A$ es no singular, ya que 0 no es un valor propio. Los valores propios de $A^{-1}$ son los números $\lambda_j^{-1}$, y están ordenados de la siguiente manera:

$$
|\lambda_n^{-1}| > |\lambda_{n-1}^{-1}| \geq \cdots \geq |\lambda_1^{-1}| > 0
$$

Consecuentemente, podemos calcular $\lambda_n^{-1}$ aplicando el método de potencia a $A^{-1}$. No es una buena idea calcular la inversa $A^{-1}$ primero y luego usar $x^{(k+1)} = A^{-1} x^{(k)}$. En su lugar, obtenemos $x^{(k+1)}$ resolviendo la ecuación

$$
A x^{(k+1)} = x^{(k)}
$$

Esto se puede hacer eficientemente usando el método de eliminación Gaussiana. Es necesario llevar a cabo la fase de factorización de la eliminación Gaussiana solo una vez y luego repetir la fase de solución cambiando los lados derechos de $x^{(0)}$ a $x^{(1)}$ a $x^{(2)}$, y así sucesivamente. Este es el método de potencia inversa.



# Algoritmo QR  de Francis
Dada una matriz $A \in \mathbb{K}^{n \times n}$, se pretende encontrar una sucesión de matrices $(A_n)_{n \in \mathbb{N}}$ convergente a la matriz triangular de Schur (en cuya diagonal aparecen los autovalores de la matriz A). La construcción de dicha sucesión se hace de la manera siguiente:

$A = A_0$. Usando factorización $QR$ , donde $Q$ es una matriz unitaria y $R$ es una matriz triangular superior con diagonal no negativa, tenemos que $A_0 = Q_0R_0$.
Además $Q_0R_0$ es semejante a $R_0Q_0$. Elijamos a $A_1 = R_0Q_0$, entonces $A_0$ tendrá los mismos valores propios que $A_1$. En general, supuesta encontrada $A_n$ se realiza la factorización $Q_nR_n$ mediante matrices de Householder [[Tópicos Selectos de Algebra Lineal#Factorización QR de Householder|(factorizacion QR de Householder)]] y $A_{n+1} = R_nQ_n$. Es decir:

$$
\begin{aligned}
A_0 &= A = Q_0R_0 \\
A_1 &= R_0Q_0 \to A_1 =  Q_1R_1 \\
A_2 &= R_1Q_1 \to A_2 =  Q_2R_2 \\
\vdots \\
A_{n-1} &= R_{n-2} \ Q_{n-2} \to A_n =  Q_nR_n
\end{aligned}
$$

De lo anterior, se observa lo siguiente:

$$
\begin{aligned}
A &= Q_0R_0  \\
  &= Q_0R_0Q_0Q_0^* = Q_0A_1Q_0^*   \\
  &= Q_0Q_1R_1Q_0^* = Q_0Q_1R_1Q_1Q_1^*Q_0^*  \\
  &= Q_0Q_1A_2Q_1^*Q_0^*   \\
\end{aligned}
$$
En general
$$
A = (Q_0Q_1 \dots Q_{n-1}) \ A_n \ (Q_{n-1}^* \dots Q_1^*Q_0^*)
$$
Tenemos entonces 
$$ A_n = (Q_0Q_1 \dots Q_{n-1})^* A_0 \ (Q_0Q_1 \dots Q_{n-1}) $$

## Observaciones
1. Los elementos de la diagonal de la matriz $A_n$ son los autovalores buscados.
2. El proceso termina cuando el mayor valor absoluto de la matriz $A_n$ (abajo de la diagonal principal) es menor que una precisión dada.
3. En general, si la matriz $A$ tiene autovalores de igual módulo, la sucesión converge a una matriz triangular por cajas, en la que cada caja contiene a los autovalores del mismo módulo.


## Observaciones
Si $\lambda_1, \lambda_2, \dots , \lambda_n$, son los autovalores de la matriz tales que:

$$
|\lambda_1| > |\lambda_2| > \dots > |\lambda_n| > 0
$$

