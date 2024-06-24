
- **Divide** el problema en uno o más subproblemas que son instancias más pequeñas del mismo problema
- **Resuelve** los subproblemas recursivamente
- **Combina** las soluciones de los subproblemas para formar una solución para el problema original.


## Recurrences
Una *recurrencia* es una ecuación que describe una función en términos de su valor en otros argumentos, generalmente más pequeños.

La forma general de una recurrencia es una ecuación o una desigualdad que describe una función sobre los enteros o reales usando la propia función, Contiene dos o mas casos, dependiendo del argumento. Si un caso implica la invocación recursiva de una función en diferentes (usualmente más pequeños) inputs, es un *recursive case*. Caso contrario es un *base case*. Puede haber cero, uno o muchas funciones que satisfagan la declaración de recurrencia. La recurrencia esta *well defined* si existe al menos una función que la satisfaga, en caso contrario es *ill defined*.


## Algorithmic recurrences

Una recurrencia $T(n)$ es *algorítmica* si, para cada constante de umbral suficientemente grande $n_0 > 0$, se cumplen las dos propiedades

1. $\forall n<n_0, \: T(n) = \Theta(1)$, es decir, 
$$ \exists c_1, c_2 \in \mathbb{R}^+ : c_1 \leq T(n) \leq c_2$$

2. $\forall n \geq n_0$, cada camino de recursión termina en una caso base definido con un número finito de llamadas recursivas.


## Divide and conquer and recurrences

