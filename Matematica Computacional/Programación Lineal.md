

Maximizar

$$
c^T x
$$
sujeto a
$$
Ax \geq b \ ,  \ x \geq 0
$$

![[Pasted image 20241117210443.png]]

**Problema**: Dado el problema en su forma canónica:
Maximizar $c_1x_1 + c_2x_2 + \dots + c_nx_n$
sujeto a 

$$
\begin{array}{cccccc} 
a_{11}x_1 & + & a_{12}x_2 & + \dots + & a_{1n}x_n & \geq b_1 \\ 
a_{21}x_1 & + & a_{22}x_2 & + \dots + & a_{2n}x_n & \leq b_2 \\ 
\vdots & & \vdots & & \vdots & \vdots \\ 
a_{m1}x_1 & + & a_{m2}x_2 & + \dots + & a_{mn}x_n & \geq b_n \end{array}
$$

$$
x_1 \geq 0, x_2 \geq 0 ,  \dots x_n \geq 0
$$

>[!tip]
>- Si es $\geq$ , se añade $+0s_i - MA_i$
>- Si es $\leq$ , se añade $+0s_i$

Paso 1: Expresar el problema en su forma estándar
Maximizar $z = c_1x_1 + c_2x_2 + \dots + c_nx_n + 0s_1 - MA_1 + 0s_2 + \dots + 0s_m - MA_m$
sujero a 

$$
\begin{array}{ccccccccc} a_{11}x_1 & + & a_{12}x_2 & + \cdots + & a_{1n}x_n & - s_1 & + A_1 & = & b_1 \\ a_{21}x_1 & + & a_{22}x_2 & + \cdots + & a_{2n}x_n & + s_2 & + A_2 & = & b_2 \\ \vdots & & \vdots & & \vdots & & \vdots & & \vdots \\ a_{m1}x_1 & + & a_{m2}x_2 & + \cdots + & a_{mn} & - s_m & + A_m & = & b_n \end{array}
$$
$$
x_1 \geq 0, \quad x_2 \geq 0, \quad \cdots, \quad x_n \geq 0
$$


- Variables no básicas: $x_1, x_2, \cdots, x_n$
- Variables básicas: $s_1, s_2, \cdots, s_m \geq 0$
- Variables artificiales: $A_1, A_2, \cdots, A_m \geq 0$

Paso 2: Construimos la siguiente tabla con los coeficientes del sistema

$$
\begin{array}{|c|cccccc|cccc|c|} \hline & x_1 & x_2 & \cdots & x_n & s_1 & A_1 & s_2 & \cdots & s_m & A_m & r \\ \hline M A_1 & a_{11} & a_{12} & \cdots & a_{1n} & -1 & 1 & 0 & \cdots & 0 & 0 & b_1 \\ M A_2 & a_{21} & a_{22} & \cdots & a_{2n} & 0 & 0 & -1 & \cdots & 0 & 0 & b_2 \\ \vdots & \vdots & \vdots & & \vdots & \vdots & \vdots & \vdots & & \vdots & \vdots & \vdots \\ M A_m & a_{m1} & a_{m2} & \cdots & a_{mn} & 0 & 0 & 0 & \cdots & -1 & 1 & b_m \\ \hline z_i & -c_1 & -c_2 & \cdots & -c_n & 0 & M & 0 & \cdots & 0 & M & M \\ \hline z_f & & & & & & & & & & & \\ \hline \end{array}
$$
Paso 3: Haciendo ceros los coeficientes M de $z_i$ mediante operaciones elementales

$$
\begin{array}{|c|cccccc|}
\hline
& & & & A_1 & \dots & A_j \\
& & & & \vdots &  & \vdots \\
\hline
z_f & -c_1-Ma_{11} & -c_2 - Ma_{12} & \dots & 0 & & 0 \\
\hline
\end{array}
$$



# Método M

## Paso 1
Para cada restricción:
- $\leq$ agregamos una variable de holgura $+s_n$
- $\geq$ restamos una variable de holgura y agregamos una variable artificial $-s_n + A_n$
- $=$ agregamos una variable artificial $+A_n$


## Paso 2
Para **minimizar**
- Valor $+ M$ por cada variable artificial $A_n$
Para **maximizar**
- Valor $- M$ por cada variable artificial $A_n$

Y despejamos la función objetivo igualando a cero $z=0$

