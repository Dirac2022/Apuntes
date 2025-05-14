


# Metodo Simplex

Dado el problema en su forma canónica:

$$
\text{Maximizar} \quad Cx
$$
sujeto a

$$
Ax \leq b
$$


- **Paso 1**: Expresar el problema en su forma estándar:

$$
\text{Maximizar} \quad z = c_1x_1 + c_2x_2 + \cdots + c_nx_n
$$

$$
\text{sujeto a}
$$

$$
\begin{array}{ccccccccc} 
a_{11}x_1 & + & a_{12}x_2 & + \cdots + & a_{1n}x_n & + & s_1 & & & = & b_1 \\ a_{21}x_1 & + & a_{22}x_2 & + \cdots + & a_{2n}x_n & + &  & s_2 &  & = & b_2 \\ 
\vdots & & \vdots & & \vdots & &  & & & & \vdots \\ 
a_{m1}x_1 & + & a_{m2}x_2 & + \cdots + & a_{mn} & + & & &  s_m  & = & b_n 
\end{array}
$$

$$
x_1 \geq 0, x_2 \geq 0, \ldots, x_n \geq 0 
$$


- **Variables no básicas**: $x_1, x_2, \ldots, x_n$
- **Variables básicas: $s_1, s_2, \ldots, s_m$

- **Paso 2**: Construimos la siguiente tabla con los coeficientes del sistema:


$$
\begin{array}{|c|ccccccccc|c|} 
\hline 
& z &x_1 & x_2 & \cdots & x_n & s_1  & s_2 & \cdots & s_m  & r \\ 
\hline 
s_1 & 0 & a_{11} & a_{12} & \cdots & a_{1n} & 1 & 0 & \cdots & 0  & b_1 \\ 
s_2 & 0 &a_{21} & a_{22} & \cdots & a_{2n} & 0 & 1 & \cdots & 0 &  b_2 \\ 
\vdots & \vdots & \vdots & & \vdots & \vdots & \vdots & \vdots & & \vdots \\ 
s_m & 0 &a_{m1} & a_{m2} & \cdots & a_{mn} & 0 & 0 & \cdots & 1  & b_m \\ 
\hline 
z & 1 & -c_1 & -c_2 & \cdots & -c_n & 0 & 0 & \cdots & 0 & 0 \\ 
\hline 
\hline 
\end{array}
$$

Aquí la solución inicial es $(0, 0, \dots, 0, b_1, b_2, \dots,  b_m)$ para obtener $z=0$

- **Paso 3**: De la fila $z$ se selecciona la columna $q$ tal que sea el menor número negativo.

- **Paso 4**: Se divide los coeficientes de la columna $r$ entre los de la columna $q$  elegida, es decir, se calculan las razones $\dfrac{b_i}{a_{iq}}$ para $a_{iq} > 0$, $i = 1, 2,  \dots, m$. Si ningún $a_{iq} > 0$, el problema no está acotado y **se detiene**.
- **Paso 5**: Se elige la fila $i$ que tenga la **menor razón positiva** obtenida en el paso anterior y se reemplaza la columna $x_q$  la fila por $s_i$, es decir, en vez de $s_i$ ahora ira $x_q$ para la siguiente tabla.
- **Paso 6**: El elemento pivote es el que se encuentra en la intersección de la fila y columna elegidos de los pasos anteriores.
- **Paso 7**: Mediante operaciones elementales se busca que el pivote sea $1$ y que los demás elementos en esa columna $q$ sean ceros.
- **Paso 8**: Si todos los coeficientes de la fila $z$ son positivos o ceros, se detiene **el problema**. En caso contrario se regresa al Paso 3 y se repite el proceso.

>[!tip] Para el Paso 7:
>- Para la fila pivote: se dividen todos sus elemento entre el elemento **pivote**, con esto se logra que el pivote sea $1$, para que las operaciones elementales por filas sea más manejable.
>- Para las demás filas:: Esto se hace para cada elemento de la fila, 

$$
\text{fila nueva} =\text{ fila antigua } - \text{ pivote de la fila} \times \text{elemento de la fila pivote} 
$$

---
# Metodo Simplex Dual

**Problema Primal**
$$
\begin{aligned}
\text{Minimizar} \quad & c^T x \\
\text{sujeto a} \quad & Ax \geq b \\
& x \geq 0
\end{aligned}
$$

**Problema Dual**
$$
\begin{aligned}
\text{Maximizar} \quad & b^T y \\
\text{sujeto a} \quad & A^T y \leq c \\
& y \geq 0
\end{aligned}
$$


## Problema Primal
Dado el problema primal:
$$
\text{Minimizar} \quad c_1x_1 + c_2x_2 + \cdots + c_nx_n
$$

$$
\text{sujeto a}
$$

$$
\begin{array}{ccccccccc} 
a_{11}x_1 & + & a_{12}x_2 & + \cdots + & a_{1n}x_n  & \geq & b_1 \\ 
a_{21}x_1 & + & a_{22}x_2 & + \cdots + & a_{2n}x_n & \geq & b_2 \\ 
\vdots & & \vdots & & \vdots & & \vdots \\ 
a_{m1}x_1 & + & a_{m2}x_2 & + \cdots + & a_{mn} & \geq & b_n 
\end{array}
$$


$$
x_1 \geq 0, x_2 \geq 0, \ldots, x_n \geq 0 
$$


## Problema Dual
- **Paso 1**: Se obtiene el siguiente problema dual


$$
\text{Maximizar} \quad b_1y_1 + b_2y_2 + \cdots + b_my_m
$$

$$
\text{sujeto a}
$$

$$
\begin{array}{ccccccccc} 
a_{11}y_1 & + & a_{21}y_2 & + \cdots + & a_{m1}y_m  & \leq & c_1 \\ 
a_{12}y_1 & + & a_{22}y_2 & + \cdots + & a_{m2}y_m & \leq & c_2 \\ 
\vdots & & \vdots & & \vdots & & \vdots \\ 
a_{1n}y_1 & + & a_{2n}y_2 & + \cdots + & a_{mn}y_m & \leq & c_n 
\end{array}
$$


$$
y_1 \geq 0, y_2 \geq 0, \ldots, y_m \geq 0 
$$

- **Paso 2**: Se resuelve el problema dual por el [[Programación Lineal#Metodo Simplex|Metodo Simplex]] 
- **Paso 3**: ==Los valores obtenidos para las variables de holgura serán los valores de las variables del Problema Primal dado.==. El valor optimo se encuentra en la misma posición en la tabla final.

## Alternativa

$$
\text{Minimizar: } z \rightarrow \text{Maximizar:} -z
$$

- Multiplicamos las restricciones por $-1$ para invertir el sentido de las desigualdades
$$
\geq \quad \rightarrow \quad \leq
$$
- En la fila $z$ tomamos el valor positivo **mas grande**
- Calculamos los cocientes como en un método simplex usual
- Tomamos el cociente **más pequeño** como en un método simplex usual
- La iteración termina cuando los valores de $x$ de la fila $z$ sean $0$
- El valor optimo de la **minimización** es el negativo del valor optimo resultante en la tabla.


----

# Metodo Simplex M


Maximizar

$$
c^T x
$$
sujeto a
$$
Ax \geq b \ ,  \ x \geq 0
$$



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

- **Paso 1**: Expresar el problema en su forma estándar
$$ \text{Maximizar } $$
$$z = c_1x_1 + c_2x_2 + \dots + c_nx_n + 0s_1 - MA_1 + 0s_2 + \dots + 0s_m - MA_m$$
$$\text{sujeto a }$$

$$
\begin{array}{ccccccccc} 
a_{11}x_1 & + & a_{12}x_2 & + \cdots + & a_{1n}x_n & - s_1  + A_1 & & & = & b_1 \\ a_{21}x_1 & + & a_{22}x_2 & + \cdots + & a_{2n}x_n & & + s_2 &  & = & b_2 \\ 
\vdots & & \vdots & & \vdots & & \vdots & & \vdots \\ 
a_{m1}x_1 & + & a_{m2}x_2 & + \cdots + & a_{mn} &  & &- s_m  + A_m & = & b_n \end{array}
$$
$$
x_1 \geq 0, \quad x_2 \geq 0, \quad \cdots, \quad x_n \geq 0
$$


	- **Variables no básicas**: $x_1, x_2, \cdots, x_n$
	- **Variables básicas**: $s_1, s_2, \cdots, s_m \geq 0$
	- **Variables artificiales**: $A_1, A_2, \cdots, A_m \geq 0$

- **Paso 2**: Construimos la siguiente tabla con los coeficientes del sistema

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

## Paso 3
Eliminar los coeficientes $M$ de las variables artificiales del renglón de la función objetivo.

## Paso 4

**Columna pivote**
- **Minimizar**: En donde esté ubicado el coeficiente más positivo del renglón de la función $z$.
- **Maximizar**: En donde esté ubicado el coeficiente más negativo del renglón de la función $z$.

**Fila pivote**: Dividimos cada valor entre los elementos de la columna pivote. Seleccionamos la fila que obtenga el menor resultado. No participan el renglón $z$, ni los valores cero o negativos.

## Paso 5
**Reducimos la columna en donde está el pivote**. Aplicando eliminación Gauss-Jordan, el pivote eliminará (convertir a cero) los demás elementos de esa columna.

## Paso 6
Validamos si alcanzamos la solución óptima en la función objetivo.
- **Minimizar**: 
	- Si hay coeficientes positivos, aplicamos de nuevo el paso 4 (columna y fila pivote).
	- Si no hay coeficientes positivos, se ha alcanzado una solución óptima.
- **Maximizar**
	- Si hay coeficientes negativos, aplicamos de nuevo el paso 4 (columna y fila pivote)
	- Si no hay coeficientes negativos, se ha alcanzado una solución óptima.

l