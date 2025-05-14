
# Complemento a 2

$$C_b(N) = b^n - N$$
Donde:
- $N$ es numero a calcular su complemento a dos
- $b$ es la base
- $n$ es el numero de dígitos o cifras de representación

## Representación en complemento a 2

- Se utiliza el bit más significativo de la palabra binaria para representar el signo (0 si es positivo y 1 si es negativo).
- Para una palabra de n bits, la capacidad de representación es de hasta $2^{n−1} − 1$ para números positivos y de $2^{n−1}$ negativos.
- Un número positivo $x$ tal que $0 \leq x \leq 2^{n−1} − 1$ es representado por la representación binaria, con bit de signo ” 0 ”.
- Un número negativo $−y$ donde $1 \leq y \leq 2^{n−1}$ es representado por la representación binaria de $2^n − y$.

## Complemento a dos en el sistema binario

### Método 1

**Una forma fácil de calcular el complemento a dos** cambiar los dígitos después de la aparición del primer $1$ de derecha a izquierda. Ejemplo

$$ C_2(11001010) \quad, \quad n = 8$$
De izquierda a derecha:

$$\begin{align*} 
0 &\rightarrow 0 \quad \text{no cambia} \\
1 &\rightarrow 1 \quad \text{no cambia} \\
0 &\rightarrow 1 \\
1 &\rightarrow 0 \\
0 &\rightarrow 1 \\
0 &\rightarrow 1 \\
1 &\rightarrow 0 \\
1 &\rightarrow 0 \\ 
\end{align*}$$

Por tanto, $C_2(11001010) = 00110110$

### Método 2

Se invierten todos los dígitos y al resultado se le suma $1$.

**Ejemplo**
$$C_2(11001010) \quad , \quad n = 8$$
$$ 11001010 \rightarrow 00110101 $$
$$ \begin{array}{r} \phantom{+} 00110101 \\ + \phantom{0} 1 \\ \hline 00110110 \\ \end{array}$$



# Resta binaria por complemento a 2

1.  El minuendo se mantiene
2. El sustraendo se cambia a su complemento a 2
3. Se suma el minuendo con el complemento a 2 del sustraendo
4. Se elimina el digito más a la izquierda del resultado

**Ejemplo**

$$ \begin{array}{r} \phantom{+} 11001111 \\ - \phantom{0} 10111101 \\ \hline \end{array}$$

$C_2(10111101) = 01000011$ , entonces

$$ \begin{array}{r} \phantom{+} 11001111 \\ + \phantom{0} 01000011 \\ \hline 100010010\end{array}$$
Por ultimo, eliminamos la cifra más significativa, por tanto

$$11001111 - 10111101 = 00010010$$

