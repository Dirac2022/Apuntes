

# Introducción
## Orden de convergencia
Sea una sucesión $\{x_k\}$, $x_k \in \mathbb{R}^n$, converge a $x^*$. Se define el orden de convergencia de $\{x_k\}$ como el máximo de los números no negativos $r$ que satisface

$$
0 \leq \underset{k \rightarrow \infty}{\lim} \frac{\|x_{k+1} - x^*\|}{\|x_k - x^*\|^r} < \infty
$$
- Si $r=1$ la sucesión se dice que converge linealmente.
- Si $r=2$ se dice que converge cuadráticamente.


Si la sucesión tiene convergencia de orden $r$, el valor $\gamma$ que satisface
$$
\gamma = \underset{k \rightarrow \infty}{\lim} \frac{\|x_{k+1} - x^*\|}{\|x_k - x^*\|^r} 
$$
se denomina tasa de convergencia o relación de convergencia. Cuando $r=1$, para que exista convergencia, $\gamma$ debe ser estrictamente menor que 1.
Si $\gamma=0$ y $r=1$, la sucesión $\{x_k\}$ se dice que converge superlinealmente. Observamos que un orden de convergencia mayor que $1$ implica convergencia superlineal.

## Teorema
Si $f : \mathbb{R} \rightarrow \mathbb{R}$ es una función continua en $[a, b]$ y $f(a)f(b) <0$, entonces existe $c \in ]a, b[$
Este teorema asegura que una ecuación no lineal tiene solución.





# Método de bisección (reducción a la mitad del intervalo)
 Si $f(a)f(b) < 0$, entonces calculamos $c = \frac{1}{2}(a + b)$ y verificamos si $f(a)f(c) < 0$. Si esto es cierto, entonces f tiene un cero en $[a, c]$. Así que renombramos $c$ como $b$ y comenzamos de nuevo con el nuevo intervalo $[a, b]$, que es la mitad del tamaño del intervalo original. Si $f(a)f(c) > 0$, entonces $f(c)f(b) < 0$, y en este caso renombramos $c$ como $a$. En cualquier caso, se ha producido un nuevo intervalo que contiene un cero de $f$, y el proceso puede repetirse. 

Las figuras muestran los dos casos, asumiendo $f(a) > 0 > f(b)$. Estas figuras dejan claro por qué el método de bisección encuentra un cero pero no todos los ceros en el intervalo $[a, b]$. Por supuesto, si $f(a)f(c) = 0$, entonces $f(c) = 0$ y se ha encontrado un cero. Sin embargo, es bastante improbable que $f(c)$ sea exactamente $0$ en la computadora debido a los errores de redondeo. Por lo tanto, el criterio de parada no debe ser si $f(c) = 0$. Se debe permitir una tolerancia razonable, como $|f(c)| < 10^{-5}$

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\biseccion intervalo izquierdo.png" alt="">
    <figcaption>Método de la bisección selecciona el intervalo izquierdo</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\biseccion intervalo derecho.png" alt="">
    <figcaption>Método de la bisección selecciona el intervalo derecho</figcaption>
    </figure>
</div>

## Algoritmo de la bisección
<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\algoritmo biseccion.png" alt="">
    <figcaption>Algoritmo de biseción</figcaption>
    </figure>
</div>

## Análisis de Error
Para analizar el método de bisección, dejemos que los intervalos sucesivos que surgen en el proceso sean $[a_0, b_0]$, $[a_1, b_1]$, y así sucesivamente. Aquí hay algunas observaciones sobre estos números:

$$a_0 \leq a_1 \leq a_2 \leq \cdots \leq b_0$$
$$b_0 \geq b_1 \geq b_2 \geq \cdots \geq a_0$$
$$b_{n+1} - a_{n+1} = \frac{1}{2} (b_n - a_n) \quad (n \geq 0) \quad (1)$$
Dado que la secuencia $[a_n]$ no es decreciente y está acotada superiormente, converge. Del mismo modo, $[b_n]$ converge. Si aplicamos repetidamente la Ecuación (1), encontramos que
$$b_n - a_n = 2^{-n}\,(b_0 - a_0)$$
Por lo tanto,
$$\lim_{n \to \infty} b_n - \lim_{n \to \infty} a_n = \lim_{n \to \infty} 2^{-n}\,(b_0 - a_0) = 0$$
Si ponemos
$$r = \lim_{n \to \infty} a_n = \lim_{n \to \infty} b_n$$
Entonces, al tomar un límite en la desigualdad $0 \geq f(a_n) f(b_n)$, obtenemos $0 \geq [f(r)]^2$, de donde $f(r) = 0$.

Supongamos que, en una etapa particular del proceso, el intervalo $[a_n, b_n]$ acaba de ser definido. Si el proceso se detiene ahora, la raíz seguramente se encuentra en este intervalo. La mejor estimación de la raíz en esta etapa no es $a_n$ ni $b_n$ sino el punto medio del intervalo:

$$c_n = (a_n + b_n) / 2$$

El error está entonces acotado de la siguiente manera:

$$|r - c_n| \leq \frac{1}{2} (b_n - a_n) = 2^{-(n+1)} (b_0 - a_0)$$

Resumiendo esta discusión, tenemos el siguiente teorema sobre el método de bisección:

## Teorema sobre el método de la bisección
Si $[a_0, b_0], [a_1, b_1], \ldots, [a_n, b_n], \ldots$ denotan los intervalos en el método de bisección, entonces los límites $\lim_{n \to \infty} a_n$ y $\lim_{n \to \infty} b_n$ existen, son iguales y representan una raíz de $f$. Si $r = \lim_{n \to \infty} c_n$ y $c_n = \frac{1}{2} (a_n + b_n)$, entonces

$$|r - c_n| \leq 2^{-(n+1)}\,(b_0 - a_0)$$


### Prueba
En efecto $\left| r - c_i \right| \le \frac{b_i - a_i}{2}$ y como $b_i - a_i = \frac{b_{i-1} - a_{i-1}}{2}$ entonces

$$
\left| r - c_i \right| \le \frac{b_i - a_i}{2} = \frac{b_{i-1} - a_{i-1}}{2^2}
$$
después de $n$ iteraciones
$$
\left| r - c_n \right| \le \frac{b - a}{2^{n+1}}
$$

![[Pasted image 20240604225018.png]]



## Número de iteraciones $n$ dada una tolerancia $\epsilon$
Del teorema anterior podemos calcular $n$ si una tolerancia para el error, $\epsilon$  es dada
$$
\frac{b-a}{2^{n+1}} < \epsilon \quad \rightarrow  \quad n+1 > \log_2 \left(\frac{b-a}{\epsilon}\right)
$$
basta que $n = \lceil \log_2 \left(\frac{b-a}{\epsilon}\right) \rceil$

# Método de la regla falsa
En el método de la bisección se elige como aproximación a $c$ el cual es el punto medio del intervalo $(a, b)$ como raíz de la función $f$. Es decir, $f(c)=0$. Si elegimos a $c$ como la intersección con el eje $X$ de la recta secante pasa por $(a, f(a))$, $(b, f(b))$, obtenemos el método de *regula falsi* o falsa posición.
![[Pasted image 20240604230831.png]]

Vemos que la pendiente del segmento $f(a)$, $f(b)$ es
$$
m = \frac{f(a) - f(b)}{a-b} =  \frac{f(a)}{a-c}
$$
Entonces
$$
c = a - f(a) \frac{b-a}{f(b) - f(a)}
$$

## Método de la regla falsa modificada
Con el método de la regla falsa, un extremo del intervalo permanece constante en cada iteración. En general, cuando la función es convexa (cóncava) creciente o decreciente, entonces al aplicar el método de falsa posición, uno de los extremos del intervalo inicial permanece constante. Esta característica impide que la convergencia sea rápida. Con el objetivo de superar estas dificultades, se hace una modificación al método de falsa posición. Cuando se observe que algún extremo del intervalo permanece constante en dos iteraciones (al menos), entonces se aplica el **algoritmo de Illinois**, el cual considera un factor $\alpha$ de la imagen del extremo que permanece constante para el cálculo del siguiente punto.

El objetivo de la introducción del factor $\alpha$ es el prevenir que algún extremo permanezca constante.


# Método de Newton

El método de Newton es un procedimiento general que se puede aplicar en muchas situaciones diversas. Cuando se especializa en el problema de localizar una raíz de una función de variable real, a menudo se llama la iteración de **Newton-Raphson**. En general, el método de Newton es más rápido que los métodos de bisección y de la secante, ya que su convergencia es cuadrática en lugar de lineal o superlineal. Una vez que la convergencia cuadrática se vuelve efectiva, es decir, los valores de la secuencia del método de Newton están suficientemente cerca de la raíz, la convergencia es tan rápida que solo se necesitan unos pocos valores más. Desafortunadamente, el método no siempre garantiza convergencia. A menudo, el método de Newton se combina con otros métodos más lentos en un método híbrido que es numéricamente globalmente convergente.

Tenemos una función $f$ cuyas raíces deben determinarse numéricamente. Sea $r$ una raíz de $f$ y sea $x$ una aproximación a $r$. Si $f''$ existe y es continua, entonces, por el teorema de Taylor,

$$0 = f(r) = f(x + h) = f(x) + hf'(x) + O(h^2)$$

donde $h = r - x$. Si $h$ es pequeño (es decir, $x$ está cerca de $r$), entonces es razonable ignorar el término $O(h^2)$ y resolver la ecuación restante para $h$. Si hacemos esto, el resultado es $h = -f(x) / f'(x)$. Si $x$ es una aproximación a $r$, entonces $x - f(x) / f'(x)$ debería ser una mejor aproximación a $r$. El método de Newton comienza con una estimación $x_0$ de $r$ y luego se define inductivamente

$$x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} \quad (n \ge 0)$$

$(1)$

## Interpretación Gráfica
El método de Newton implica linearizar la función. Es decir, $f$ fue reemplazada por una función lineal. La forma habitual de hacer esto es reemplazar $f$ por los dos primeros términos de su serie de Taylor. Así, si

$$ f(x) = f(c) + f'(c)(x - c) + \frac{1}{2} f''(c)(x - c)^2 + \cdots $$

entonces la linearización (en $c$) produce la función lineal

$$ \ell(x) = f(c) + f'(c)(x - c) $$

Observa que $\ell$ es una buena aproximación de $f$ en la vecindad de $c$, y de hecho tenemos $\ell(c) = f(c)$ y $\ell'(c) = f'(c)$. Así, la función lineal tiene el mismo valor y la misma pendiente que $f$ en el punto $c$. Entonces, en el método de Newton estamos construyendo la tangente a la curva $f$ en un punto cerca de $r$, y encontrando donde la línea tangente interseca el eje $x$.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\metodo-newton interpretacion-geometrica.png" alt="">
    <figcaption>Interpretación geométrica del método de Newton</figcaption>
    </figure>
</div>

Teniendo en cuenta esta interpretación gráfica, podemos imaginar fácilmente funciones y puntos de partida para los cuales la iteración de Newton falla. Tal función se muestra en la siguiente figura. En este ejemplo, la forma de la curva es tal que para ciertos valores iniciales, la secuencia $[x_n]$ diverge. Por lo tanto, cualquier declaración formal sobre el método de Newton implica una suposición de que $x_0$ está lo suficientemente cerca de un cero o que el gráfico de f tiene una forma prescrita.

<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\metodo-newton no-convergencia.png" alt="">
    <figcaption>Ejemplo de no convergencia</figcaption>
    </figure>
</div>


## Análisis de Error
Por errores, nos referimos a las cantidades
$$e_n = x_n - r$$
(No estamos considerando errores de redondeo). Supongamos que $f''$ es continua y $r$ es una raíz simple de $f$, de modo que $f(r) = 0 \neq f'(r)$. De la definición de la iteración de Newton, tenemos

$$e_{n+1} = x_{n+1} - r = x_n - \frac{f(x_n)}{f'(x_n)} - r$$
$$= e_n - \frac{f(x_n)}{f'(x_n)} = e_n \frac{f'(x_n) - f(x_n)}{f'(x_n)} \quad (2)$$

Por el teorema de Taylor, tenemos
$$0 = f(r) = f(x_n - e_n) = f(x_n) - e_n f'(x_n) + \frac{1}{2} e_n^2 f''(\xi_n)$$

donde $\xi_n$ es un número entre $x_n$ y $r$. Una reorganización de esta ecuación produce

$$e_n f'(x_n) - f(x_n) = \frac{1}{2} f''(\xi_n) e_n^2$$

Colocando esto en la Ecuación (2) lleva a

$$e_{n+1} = \frac{1}{2} \frac{f''(\xi_n)}{f'(x_n)} e_n^2 \approx \frac{1}{2} \frac{f''(r)}{f'(r)} e_n^2 = C e_n^2 \quad (3)$$

Esta ecuación nos dice que $e_{n+1}$ es aproximadamente una constante por $e_n^2$. Esta situación deseable se llama convergencia cuadrática. Explica el aparente doblamiento de la precisión con cada iteración del método de Newton en muchas aplicaciones.

Aún no hemos establecido la convergencia del método. Por la Ecuación (3), la idea de la prueba es simple: si $e_n$ es pequeño y si el factor $\frac{1}{2} f''(\xi_n) / f'(x_n)$ no es demasiado grande, entonces $e_{n+1}$ será más pequeño que $e_n$. Definimos una cantidad $c(\delta)$ dependiente de $\delta$ por

$$c(\delta) = \frac{1}{2} \frac{\max_{|x-r|\leq \delta} |f''(x)|}{\min_{|x-r|\leq \delta} |f'(x)|} \quad (\delta > 0) \quad (4)$$

Seleccionamos $\delta$ lo suficientemente pequeño para asegurarnos de que el denominador en la Ecuación (4) sea positivo, y luego, si es necesario, disminuimos $\delta$ para que $\delta c(\delta) < 1$. Esto es posible porque a medida que $\delta$ converge a 0, $c(\delta)$ converge a $\frac{1}{2} |f''(r)| / |f'(r)|$, y por lo tanto $\delta c(\delta)$ converge a 0. Habiendo fijado $\delta$, establecemos $\rho = \delta c(\delta)$. Supongamos que comenzamos la iteración de Newton con un punto $x_0$ que satisface $|x_0 - r| \leq \delta$. Entonces $|e_0| \leq \delta$ y $|e_0 c(\delta)| \leq |e_0| \rho < |e_0| \leq \delta$.

Por lo tanto, la Ecuación (3) produce

$$|x_1 - r| = |e_1| \leq e_0^2 c(\delta) \leq |e_0| |e_0| c(\delta) \leq |e_0| \rho < |e_0| \leq \delta$$

Esto muestra que el siguiente punto, $x_1$, también se encuentra dentro de $\delta$ unidades de $r$. Por lo tanto, el argumento puede repetirse, con los resultados

$$|e_1| \leq \rho |e_0|$$
$$|e_2| \leq \rho |e_1| \leq \rho^2 |e_0|$$
$$|e_3| \leq \rho |e_2| \leq \rho^3 |e_0|$$

En general, tenemos

$$|e_n| \leq \rho^n |e_0|$$

Dado que $0 \leq \rho < 1$, tenemos $\lim_{n \to \infty} \rho^n = 0$, y así $\lim_{n \to \infty} e_n = 0$. Resumiendo, obtenemos el siguiente teorema sobre el método de Newton.



## Teorema sobre el Método de Newton

Sea $f''$ continua y sea $r$ una raíz simple de $f$. Entonces, existe un vecindario de $r$ y una constante $C$ tal que si el método de Newton se inicia en ese vecindario, los puntos sucesivos se acercan continuamente a $r$ y satisfacen

$$|x_{n+1} - r| \leq C (x_n - r)^2 \quad (n \ge 0)$$


# Método de la secante
Recodemos que la iteración de Newton esta definida por la ecuación
$$
x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
$$
Una de los inconvenientes del método de Newton es que involucra la derivada de la función de cuyo cero se busca. Para superar esta desventaja se han propuesto algunos métodos. Por ejemplo

## Iteración de Steffensen
Esta iteración nos brinda otro enfoque para resolver el problema
$$
x_{n+1} = x_n - \frac{[f(x_n)]^2}{f(x_n + f(x_n)) - f(x_n)}
$$


## Método de la secante
Otro enfoque sería reemplazar la derivada de la función $f'(x)$ por un **cociente de diferencias** como
$$
f'(x_n) \approx \frac{f(x_n) - f(x_{n-1})}{x_n - x_{n-1}}
$$
Cuando se hace este reemplazo, el algoritmo resultante se llama método de la secante.
La ecuación de iteración es la siguiente
$$
x_{n+1} = x_{n} - f(x_n)\left[\frac{x_n - x_{n-1}}{f(x_n) - f(x_{n-1})}\right] \quad \quad (n \geq 1)
$$

# Método del punto fijo

## Iteración Funcional
El método de Newton y el método de Steffensen son ejemplos de procedimientos mediante los cuales se calcula una secuencia de puntos mediante una fórmula de la forma

$$
x_{n+1} = F(x_n) \quad (n \geq 0) \tag{1}
$$

El algoritmo definido por tal ecuación se llama **iteración funcional**. En el método de Newton, la función $F$ está dada por

$$
F(x) = x - \frac{f(x)}{f'(x)}
$$

Muchos otros ejemplos del procedimiento general de iteración funcional podrían ser citados, y estudiaremos el tema brevemente.

Nuestro interés reside principalmente en aquellos casos donde $\lim_{n \to \infty} x_n$ existe. Supongamos entonces que

$$
\lim_{n \to \infty} x_n = s
$$

¿Cuál es la relación entre $s$ y $F$? Si $F$ es continua, entonces

$$
F(s) = F\left( \lim_{n \to \infty} x_n \right) = \lim_{n \to \infty} F(x_n) = \lim_{n \to \infty} x_{n+1} = s
$$

Así, $F(s) = s$, y llamamos a $s$ un **punto fijo** de la función $F$. Podríamos pensar en un punto fijo como un valor al cual la función "se adhiere" en el proceso iterativo.

## Función contractiva
A menudo, un problema matemático puede ser reducido al problema de encontrar un punto fijo de una función. Tenemos la intención de analizar el caso más simple cuando $F$ mapea algún conjunto cerrado $C \subseteq \mathbb{R}$ en sí mismo. El teorema a probar concierne a **mapeos contractivos**. Un mapeo (o función) $F$ se dice que es **contractivo** si existe un número $\lambda$ menor que 1 tal que

$$
|F(x) - F(y)| \leq \lambda |x - y| \tag{2}
$$

para todos los puntos $x$ y $y$ en el dominio de $F$. Como se ilustra en la Figura 3.7, la distancia entre $x$ e $y$ se mapea en una distancia más pequeña entre $F(x)$ y $F(y)$ mediante la función contractiva $F$.

![[funcion contractiva.png]]

## Teorema del Mapeo Contractivo
Sea $C$ un subconjunto cerrado de la recta real. Si $F$ es un mapeo contractivo de $C$ en $C$, entonces $F$ tiene un único punto fijo. Además, este punto fijo es el límite de cada secuencia obtenida de la Ecuación (1) con un punto inicial $x_0 \in C$.

Usamos la propiedad contractiva (2) junto con la Ecuación (1) para escribir

$$
|x_n - x_{n-1}| = |F(x_{n-1}) - F(x_{n-2})| \leq \lambda |x_{n-1} - x_{n-2}| \tag{3}
$$

Este argumento puede repetirse para obtener

$$
|x_n - x_{n-1}| \leq \lambda |x_{n-1} - x_{n-2}| \leq \lambda^2 |x_{n-2} - x_{n-3}| \leq \cdots \leq \lambda^{n-1} |x_1 - x_0|
$$

Dado que $x_n$ se puede escribir en la forma

$$
x_n = x_0 + (x_1 - x_0) + (x_2 - x_1) + \cdots + (x_n - x_{n-1})
$$

vemos que la secuencia $\{ x_n \}$ converge si y solo si la serie

$$
\sum_{n=1}^\infty (x_n - x_{n-1})
$$

converge. Para probar que esta serie converge, basta probar que la serie

$$
\sum_{n=1}^\infty |x_n - x_{n-1}|
$$

converge. Esto es fácil porque podemos usar la prueba de comparación y el trabajo anterior:

$$
\sum_{n=1}^\infty |x_n - x_{n-1}| \leq \sum_{n=1}^\infty \lambda^{n-1} |x_1 - x_0| = \frac{1}{1 - \lambda} |x_1 - x_0|
$$

Dado que la secuencia converge, sea $s = \lim_{n \to \infty} x_n$. Entonces $F(s) = s$, como se señaló anteriormente. (Observe que la propiedad contractiva implica la continuidad de $F$.) En cuanto a la unicidad del punto fijo, si $x$ e $y$ son puntos fijos, entonces

$$
|x - y| = |F(x) - F(y)| \leq \lambda |x - y|
$$

Dado que $\lambda < 1$, $|x - y| = 0$. Finalmente, note que el punto $s$ que se obtiene pertenece a $C$ ya que es el límite de una secuencia que yace en $C$.

## Análisis de Errores

Ahora analicemos los errores en el proceso de iteración funcional. Supongamos que $F$ tiene un punto fijo, $s$, y que una secuencia $\{ x_n \}$ ha sido definida por la fórmula $ x_{n+1} = F(x_n) $. Definamos

$$
e_n = x_n - s
$$

Si $F'$ existe y es continua, entonces por el Teorema del Valor Medio,

$$
x_{n+1} - s = F(x_n) - F(s) = F'(\xi_n)(x_n - s)
$$

o
$$
e_{n+1} = F'(\xi_n)e_n
$$

donde $\xi_n$ es un punto entre $x_n$ y $s$. La condición $|F'(x)| < 1$ para todo $x$ asegura que los errores disminuyen en magnitud. Si $e_n$ es pequeño, entonces $\xi_n$ está cerca de $s$, y $F'(\xi_n) \approx F'(s)$. Se esperaría una convergencia rápida si $F'(s)$ es pequeño. Una situación ideal sería $F'(s) = 0$. En ese caso, un término adicional en la serie de Taylor será útil. Para manejar varios casos a la vez, supongamos que $q$ es un entero tal que

$$
F^{(k)}(s) = 0 \quad \text{para} \quad 1 \leq k < q \quad \text{pero} \quad F^{(q)}(s) \neq 0
$$

Por la serie de Taylor para $F(x_n)$ expandida alrededor de $s$, tenemos

$$
\begin{aligned}
e_{n+1} &= x_{n+1} - s = F(x_n) - F(s) \\
&= F(s + e_n) - F(s) \\
&= \left[ F(s) + e_n F'(s) + \frac{1}{2} e_n^2 F''(s) + \cdots \right] - F(s) \\
&= e_n F'(s) + \frac{1}{2} e_n^2 F''(s) + \cdots + \frac{1}{(q-1)!} e_n^{q-1} F^{(q-1)}(s) + \frac{1}{q!} e_n^q F^{(q)}(\xi_n)
\end{aligned}
$$

y por lo tanto

$$
e_{n+1} = \frac{1}{q!} e_n^q F^{(q)}(\xi_n)
$$

Si sabemos que $\lim_{n \to \infty} x_n = s$, entonces la Ecuación (4) implica que

$$
\lim_{n \to \infty} \left| \frac{e_{n+1}}{e_n^q} \right| = \frac{1}{q!} F^{(q)}(s)
$$
