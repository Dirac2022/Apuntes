
La teoría de optimización o programación matemática está constituida por un conjunto de resultados y métodos numéricos enfocados a encontrar e identificar al mejor candidato de entre una colección de alternativas, sin tener que enumerar y evaluar
explícitamente todas esas alternativas. 
En general un problema de optimización consiste en buscar valores para determinadas variables, de forma que cumpliendo un conjunto de requisitos, representados en general mediante ecuaciones y/o inecuaciones algebraicas (las restricciones del problema), proporcionan el mejor (mayor o menor) valor posible para una función que es
utilizada para medir el rendimiento del sistema en estudio.


Elementos de optimización
- Función objetivo
- Variables independientes
- Restricciones

Tipos de problemas
- Problemas de Programación Lineal
- Problemas de Programación no Lineal

Clasificación según el tipo de problema
- Optimización continua
- Optimización Discreta

# Solución factible
Diremos que $x$ es una solución factible si cumple todas sus restricciones.

# Conjunto factible
Se define región o conjunto factible $\Omega$ al conjunto de todas las soluciones factibles.

# Mínimo global
$x_0$ es un mínimo global si
$$
\forall \, x \in \Omega \, , \ f(x_0) \leq f(x)
$$

# Máximo global
$x_0$ es un máximo global si
$$
\forall \, x \in \Omega \, , \ f(x_0) \geq f(x)
$$

# Solución óptima
- $x_0$ es una solución óptima si es un mínimo global y el objetivo del problema es minimizar.
- $x_0$ es una solución óptima si es un máximo global y el objetivo del problema es maximizar.

# Valor óptimo
Si $x_0$ es una solución óptima, entonces $f(x_0)$ es el valor óptimo.


# Mínimo local
$x_0$ es un mínimo local si
$$
\exists \ \varepsilon > 0 \ , \ \forall  \, x \in \Omega \, , |x-x_0| < \varepsilon \rightarrow \ f(x_0) \leq f(x)
$$

# Máximo local
$x_0$ es un máximo local si
$$
\exists \ \varepsilon > 0 \ , \ \forall  \, x \in \Omega \, , |x-x_0| < \varepsilon \rightarrow \ f(x_0) \geq f(x)
$$



