Un problema de programación lineal se dice que es de programación lineal entera cuando se exige que todas las variables de decisión tengan valores enteros. Por ejemplo:


$$
\text{Maximizar} \quad 6x_1 + 3x_2
$$
$$
\text{sujeto a}
$$
$$
\begin{array}{ccccccc} 
x_1 & + & 4x_2  & \leq & 90 \\ 
4x_1 & + & 6x_2 & \leq & 80 \\  
& & x_1 \ , x_2 & \geq &0 \\
& & x_1 \ , x_2 & \in & \mathbb{Z}   
\end{array}
$$

## Programacion Lineal Entera Mixta

Un problema de programación lineal se dice que es de programación lineal entera mixta cuando algunas variables de decisión toman valores enteros y otros pueden asumir cualquier numero real no negativo (cualquier valor continuo).

## Algoritmo Branch and Bound

- Consiste en hacer una partición del conjunto de soluciones admisibles en subconjuntos propios que no se traslapen.
- Luego se calculan los límites para el valor de la mejor solución en cada subconjunto.
- Producto del análisis se eliminan ciertos subconjuntos. De esta manera se enumeran parcialmente todas las soluciones admisibles existentes.

