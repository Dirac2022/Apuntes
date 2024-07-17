
# El Sistema Posicional

Sea una base $\beta \in \mathbb{N}$ fija con $\beta \geq 2$, y sea $x$ un número real con un número finito de dígitos $x_k$ con $0 \leq x_k < \beta$ para $k = -m, ..., n$. 

**Notación** $x_{\beta} = (-1)^s [x_nx_{n-1}...x_1x_0 . x_{-1}x_{-2}...x_{-m}], \quad x_n \neq 0$


La notación anterior se llama *representación posicional de $x$ respecto de la base $\beta$*. El punto entre $x_0$ y $x_{-1}$ se llama punto decimal si la base es $10$, *punto binario* si la base es $2$, mientras que $s$ depende del signo de $x$ ($s=0$, si $x$ es positivo, y $1$ si es negativo). También
$$ x_{\beta} = (-1)^s \left(\sum_{k=-m}^{n} x_k\beta^k \right) $$



**Cualquier número real puede ser aproximado por números que tienen una representación finita**. En efecto, teniendo una base $\beta$ fija, se cumple la siguiente propiedad.
$$\forall \epsilon > 0, \forall x_{\beta} \in \mathbb{R}, \exists y_{\beta} \in \mathbb{R} \quad \text{ tal que } |y_{\beta} - x_{\beta}| < \epsilon $$
donde *$y_{\beta}$ tiene una representación posicional finita*.

De hecho, sea el número positivo $x_{\beta} = x_nx_{n-1}...x_1x_0 . x_{-1}x_{-2}...x_{-m}$ . . . con un número de dígitos finito o infinito, para cualquier $r \geq 1$ se pueden construir dos números
$$ x_{\beta}^{(l)} = \sum_{k=0}^{r-1} x_{n-k}\beta^{n-k} \quad ,  \quad x_{\beta}^{(u)} = x_{\beta}^{(l)} + \beta^{n-r+1} $$
teniendo $r$ dígitos, tal que $x_{\beta}^{(l)} < x_{\beta} x_{\beta}^{(u)}$ y   $x_{\beta}^{(u)} - x_{\beta}^{(l)} = \beta^{n-r+1}$. Si $r$ se elige de tal manera que $\beta^{n-r+1} < \epsilon$, y luego tomando $y_b$ igual a $x_{\beta}^{(l)}$ o $x_{\beta}^{(u)}$ se obtiene la desigualdad deseada. Este resultado legitima la representación computacional de números reales.


# El sistema de números de punto-flotante

Supongamos que una computadora dada tiene $N$ posiciones de memoria para almacenar cualquier número. La manera más natural representar un número real $x$ diferente de $0$ es fijar una posición para su signo, $N-k+1$ posiciones para los dígitos enteros y $k$ posiciones para los dígitos más allá del punto, de manera que
$$ x = (-1)^s \cdot [a_{N-2}a_{N-3}...a_{k} . a_{k-1} ... a_0] \quad, $$
$s = 0, 1$. Note que una posición de memoria es equivalente a bit de almacenamiento solo cuando $\beta = 2$. El conjunto de números de este tipo se llama *sistema de punto fijo*. La ecuación anterior también se puede expresar como
$$ x = (-1)^s \cdot \beta^{-k} \sum_{j=0}^{N-2} a_j \beta^{j}  \quad \quad (*)$$

Expresado en forma detallada
$$ \underbrace{{N-2}\beta^{N-2-k} + a_{N-3}\beta^{N-3-k} + a_{k+1}\beta^{1} + a_{k}\beta^{0}}_{\text{integer part}} \cdot a_{k-1}\beta^{-1} + a_{1}\beta^{1-k} + a_{0}\beta^{-k}$$
y por lo tanto esta representación equivale a fijar un factor de escala para todos los números representables.
El uso de punto fijo limita fuertemente el valor del mínimo y máximo números que pueden ser representados en la computadora, a menos que se emplee un número muy grande $N$ de posiciones de memoria.

 Este inconveniente puede ser fácilmente superado si se permite que la escala en  $(*)$ varíe. En tal caso, dado un número real $x$ no nulo, su representación en *punto-flotante* esta dado por
	
 
$$x = (-1)^s \cdot (0 . a_1 a_2 ... a_t) \cdot \beta^e = (-1)^s \cdot m \cdot \beta^{e-t} $$
donde $t \in \mathbb{N}$ es el número de dígitos significativos permitidos $a_i$ , $0 \leq a_i \leq \beta - 1$, $m=a_1a_2 ... a_t$ un número entero llamado *mantisa* tal que $0 \leq m \leq \beta^t - 1$  y $e$ es un número entero llamado *exponente*. ^882478

4 digitos para la parte fraccionaria

$$ 0.245698 \times 10^5 $$
$$ 24.5698 \times 10^3 $$


Claramente el exponente puede variar entre un intervalo finito de valores admisibles: dejamos que $L \leq e \leq U$ (típicamente $L < 0$ y $U>0$). El número de posiciones $N$ esta ahora distribuido entre *el signo* (una posición), *los dígitos significativos* ($t$ posiciones) y *los dígitos para el exponente* (las $N-t-1$ posiciones restantes). El número $0$ tiene una representación separada. 

Típicamente, en la computadora hay dos formas disponibles para la representación de número en *punto-flotante*: precisión *simple* (single) y *doble*. En el caso de representación binaria:

$N=32$ bits *(single precision)*

<div style="text-align: center;">
    <img src="https://media.geeksforgeeks.org/wp-content/uploads/Single-Precision-IEEE-754-Floating-Point-Standard.jpg">
</div>

$N=64$ bits *(double precision*


<div style="text-align: center;">
	<figure>
    <img src="https://media.geeksforgeeks.org/wp-content/uploads/Double-Precision-IEEE-754-Floating-Point-Standard-1024x266.jpg" width=650>
    <figcaption></figcaption>
    </figure>
</div>


Denotemos por
$$ \mathbb{F}(\beta, t, L, U) = {0} \: \cup \left\{ x \in \mathbb{R} : x = (-1)^s \beta^e \sum_{i=1}^{t}a_i\beta^{-i} \right\}$$

$$ (1 \times 2^{-1} + 1 \times 2^{-2} + 1 \times 2^{-3} ... + 1 \times 2^{-t}) \times \beta^e $$
$$  1.0100 \times 2^4$$


el conjunto de números en *punto-flotante* con $t$ dígitos significativos, base $\beta \geq 2$, $0 \leq a_i \leq \beta - 1$, y rango $(L, \: U)$ con $L \leq e \leq U$.

Para garantizar la *unicidad* en una representación numérica, se asume típicamente que
- -$a_1 \neq 0$ y $m \geq \beta^{t-1}$. 
- En tal caso $a_1$ se llama el *principal dígito significativo*, mientras $a_t$ es el *ultimo dígito significativo* y la representación de $x$ se llama **normalizada**. 
- La *mantisa* $m$ ahora esta variando entre $b^{t-1}$ y $b^t - 1$.

**Por ejemplo**, para el caso $\mathbb{F} (10, 4, -1, 4)$ sin el supuesto que $a_1 \neq 0$, el número $1$ admite las siguientes representaciones:

Como $e$ varía entre $[-1, 4]$ 

- Para $e=-1 \rightarrow$ no hay representación
- Para $e=0 \rightarrow$ no hay representación
- Para $e=1 \rightarrow$ $1 = 0.1000 \cdot 10^{1}$  , $\quad 10^{-1} ( 1 \times 10^{-1} + 0 \times 10^{-2} + 0 \times 10^{-3} + 0 \times 10^{-4})$
- Para $e=2 \rightarrow$ $1 = 0.0100 \cdot 10^{2}$  , $\quad 10^{-1} ( 0 \times 10^{-1} + 1 \times 10^{-2} + 0 \times 10^{-3} + 0 \times 10^{-4})$
- Para $e=3 \rightarrow$ $1 = 0.0010 \cdot 10^{3}$  , $\quad 10^{-1} ( 0 \times 10^{-1} + 0 \times 10^{-2} + 1 \times 10^{-3} + 0 \times 10^{-4})$
- Para $e=4 \rightarrow$ $1 = 0.0001 \cdot 10^{4}$  , $\quad 10^{-1} ( 0 \times 10^{-1} + 0 \times 10^{-2} + 0 \times 10^{-3} + 1 \times 10^{-4})$

Para tener siempre una representación única se asume también que el número *zero* tiene su propio signo ($s=0$). Podemos notar que si $$x \in \mathbb{F}(\beta, t, L, U) \rightarrow -x \in \mathbb{F}(\beta, t, L, U)$$
Además, se cumplen los siguientes límites superior e inferior para el valor absoluto de $x$
$$ x_{min} = \beta^{L-1} \leq |x| \leq \beta^{U}(1-\beta^{-t}) = x_{max}$$
*Aclaración-demostración*: puesto que: 
- $x_{min} = \beta^e \cdot (a_1\beta^{-1})$ ya que $e$ toma el menor valor $L$ , $a_1$ toma el menor valor posible $1 \neq 0$ y los demás $a_i = 0$, entonces $x_{min} = \beta^L \cdot \beta^{-1}$
- $x_{max}$ = $\beta^e \cdot \sum_{i=1}^{t}a_i\beta^{-i}$ donde $e$ toma el máximo valor $U$ y $a_i = \beta - 1$  $\forall \: i = 1, \cdots , t$ . Entonces la suma se reduce a $1-\beta^{-t}$

La cardinalidad de $\mathbb{F}$ es entonces (*por demostrar*)

$$ card ( \mathbb{F} ) = 2(\beta - 1)\beta^{t-1} (U - L + 1) + 1 $$
## Floating-point de-normalized
Resulta que no es posible representar cualquier número (a parte del $0$) cuyo valor absoluto sea menor que $x_{min}$, Esta ultima limitación se puede superar completando $\mathbb{F}$ con el conjunto $\mathbb{F}_D$ de los números en *punto-flotante denormalizados* obtenidos removiendo el supuesto que $a_1$ no es nulo, solo para los números que se refieren al exponente mínimo $L$. De esta manera la unicidad en la representación no se pierde y es posible generar números que tengan la mantisa entre $1$ y $\beta^{t-1} - 1$ y pertenezcan al intervalo $(-\beta^{L-1} , \, \beta^{L-1})$. El valor más pequeño en este conjunto tiene un valor absoluto igual a $\beta^{L-t}$.


#### Ejemplo
Los números positivos en el conjunto $\mathbb{F} (2, 3, -1, 2)$ son

| 0.111                                  | 0.110                                 | 0.101                                  | 0.100                                 |
| -------------------------------------- | ------------------------------------- | -------------------------------------- | ------------------------------------- |
| $(0.111) \cdot 2^{2} = \dfrac{7}{2}$   | $(0.110) \cdot 2^{2} = 3$             | $(0.101) \cdot 2^{2} = \dfrac{5}{2}$   | $(0.100) \cdot 2^{2} = 2$             |
| $(0.111) \cdot 2^{1} = \dfrac{7}{4}$   | $(0.110) \cdot 2^{1} = \dfrac{3}{2}$  | $(0.101) \cdot 2^{1} = \dfrac{5}{4}$   | $(0.100) \cdot 2^{1} = 1$             |
| $(0.111) \cdot 2^{0} = \dfrac{7}{8}$   | $(0.110) \cdot 2^{0} = \dfrac{3}{4}$  | $(0.101) \cdot 2^{0} = \dfrac{5}{8}$   | $(0.100) \cdot 2^{0} = \dfrac{1}{2}$  |
| $(0.111) \cdot 2^{-1} = \dfrac{7}{16}$ | $(0.110) \cdot 2^{-1} = \dfrac{3}{8}$ | $(0.101) \cdot 2^{-1} = \dfrac{5}{16}$ | $(0.100) \cdot 2^{-1} = \dfrac{1}{4}$ |

En este caso se representan los números del conjunto $\mathbb{F}$ normalizados. Cuando consideramos también los números positivos *denormalizados* debemos completar el conjunto agregando los siguientes números:

$$
(.011)_2 \ \cdot 2^{-1} =  \frac{3}{16} , \  (.010)_2 \ \cdot 2^{-1} =  \frac{1}{8} , \ (.001)_2 \ \cdot 2^{-1} =  \frac{1}{16}
$$

De acuerdo con lo establecido anteriormente, el número más pequeño denormalizado es $\beta^{L-t} = 2^{-1-3} = 1/16$

# Distribución de números en punto-flotante

**Los números en *punto-flotante* no están equidistamente espaciados sobre la recta real**, pero se vuelven densos cerca del número representable más pequeño. 
## Machine epsilon
El espacio entre entre un número $x \in \mathbb{F}$ y su siguiente vecino $y \in \mathbb{F}$, donde $x, \, y \neq 0$, es al menos $\beta^{-1} \epsilon_M |x|$ y a lo mucho $\epsilon_M |x|$
$$\epsilon_M = \beta^{1-t}$$ es el *epsilon de la máquina*. Este último representa **la distancia entre el número $1$ y el número en punto flotante más cercano** y por tanto, representa el número más pequeño de $\mathbb{F}$ tal que $1 + \epsilon_M > 1$.

En cambio, **al fijar un intervalo de la forma $[\beta^e, \beta^{e+1}]$, los números de $\mathbb{F}$ que pertenecen a tal intervalo están equidistamente espaciados y tienen una distancia igual a $\beta^{e-t}$**. 

- Disminuir (o aumentar) en uno el exponente da lugar a una disminución (o aumento) de un factor $\beta$ de la distancia entre números consecutivos.

## relative distance
A diferencia de la distancia absoluta, la *distancia relativa* entre dos números consecutivos tiene un comportamiento periódico que solo depende de la mantisa $m$. Sea $(-1)^sm(x)\beta^{e-t}$, la distancia relativa es
$$\frac{\Delta x}{x} = \frac{(-1)^s\beta^{e-t}}{(-1)^s m(x) \beta^{e-t}} = \frac{1}{m(x)}$$

Dentro del intervalo $[\beta^e , \, \beta^{e+1}]$, la razón esta disminuyendo a medida que $x$ aumenta, ya que la representación normalizada de la mantisa varía dentro de $[\beta^{t-1} , \, \beta^t - 1 )$. Sin embargo, tan pronto como $x = \beta^{e+1}$, la distancia relativa regresa al valor $\beta^{1-t}$  y empieza a decrecer en los intervalos sucesivos. Este fenómeno oscilatorio se llama ***precision titubeante (wobbling precision)*** y cuanto mayor sea la base $\beta$, más pronunciado será el efecto. **Esta es otra razón por la que se prefieren emplear bases pequeñas en las computadoras**.


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\ejemplo variacion distancia relativa.png">
    <figcaption></figcaption>
    </figure>
</div>

## Exceptional values

$$\begin{array}{ccc} \hline value & exponent & mantisa  \\ 
\hline
\pm 0 & L-1 & 0 \\
\pm \infty & U+1 & 0 \\
NaN & U+1 & \neq 0  \\ \hline \end{array}$$

Es decir:
- $\pm 0 = (-1)^s \cdot  0 \cdot \beta^{(L-1)}$
- $\pm \infty = (-1)^s \cdot \ 0 \cdot \beta^{U+1}$
- $NaN = (-1)^s \cdot \ \neq 0 \cdot \beta^{U+1}$


# Redondeo de un número real en su representación en máquina

Dado  que $\mathbb{F} \subset \mathbb{R}$, no se pueden representar todos los números en una recta real. Además,  dados $x, \, y \in \mathbb{F}$, el resultado de una operación entre estos número no pertenece necesariamente a $\mathbb{F}$. Para resolver el primer problema redondeemos $x$ de tal manera que pertenezca a $\mathbb{F}$. 

Dado $x \in \mathbb{R}$ en *notación posicional normalizada* reemplacemos $x$ por su representación $fl(x)$ en $\mathbb{F}$, definido como
$$fl(x) = (-1)^s (0.a_1a_2 \cdots \tilde{a}_t) \cdot \beta^e \, , \quad 
\tilde{a}_t = \left\{ \begin{array}{ll} a_t \: , & a_{t+1} < \beta / 2 , \\
a_t + 1 \: , & a_{t+1} \geq \beta / 2
\end{array} \right.$$

La función de mapeo $fl : \mathbb{R} \rightarrow \mathbb{F}$ es la más comúnmente utilizada y se llama *redondeo* (**en el redondeo por truncamiento se tomaría mas trivialmente $\tilde{a}_t = a_t$**). La función cumple la *propiedad de monotonicidad*^redondeo



## Overflow and underflow
Todo lo descrito hasta ahora se aplica solo para los números que en la [[#^882478|expresión]] tienen un exponente $e$ dentro del rango de $\mathbb{F}$. Si, de hecho, $x \in (\infty, \, -x_{max}) \cup (x_{max}, \, \infty)$ el valor $fl(x)$ no esta definido, mientras que si $x \in (-x_{min}, \, x_{min})$ la operación de *redondeo* esta definida de todas formas (*incluso en ausencia de números denormalizados*). En el primer caso, si $x$ es el resultado de una operación sobre números en $\mathbb{F}$, hablamos de *desbordamiento (overflow)*, en el segundo caso sobre *subdesbordamiento (underflow)*, o (*desbordamiento elegante* si se consideran los números denormalizados). El desbordamiento es manejado por el sistema a través de una interrupción del programa en ejecución.

Se pueden diferenciar 5 regiones en $F$:
1. Los números negativos menores que $−x_{max}$, región denominada *overflow negativo*.
2. Los números negativos mayores que $−x_{min}$, región denominada *underflow negativo*.
3. El cero.
4. Los números positivos menores que $x_{min}$, región denominada *underflow positivo*.
5. Los números positivos mayores que $x_{max}$, región denominada *overflow positivo*.


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\overflow y underflow.png">
    <figcaption></figcaption>
    </figure>
</div>

## Absolute and relative error
Podemos cuantificar el error, absoluto o relativo, que se comete al sustituir $fl(x)$ por $x$. El resultado siguiente puede ser demostrado

### Propiedad
Si $x \in \mathbb{R}$ tal que $x_{min} \leq |x| \leq x_{max}$, entonces
$$ fl(x) = x(1 + \delta) \quad , \quad |\delta| \leq u \quad (**)$$
Donde 
#### roundoff unit or machine precision
$$ u = \frac{1}{2} \beta^{1-t} = \frac{1}{2} \epsilon_M$$

es la llamada **unidad de redondeo (o precisión de la máquina)**.



Como consecuencia de $(**)$, se cumplen las siguientes cotas para el error relativo y absoluto

### Relative error
$$ E_{rel} (x) = \frac{|x - fl(x)|}{|x|} \leq u \, ,$$
### Absolute error
$$ E(x) = |x - fl(x)| \leq \beta^{e-t} \, | (a_1 ... a_t . a_{t+1} ... ) - (a_1 ... \tilde{a}_t) | $$

De la  [[#^redondeo|expresión]], se sigue que
$$|(a_1a_2 ...a_t . a_{t+1} ...) - (a1 ... \tilde{a}_t)| \leq \beta^{-1} \frac{\beta}{2} \: , $$
de donde
$$ E(x) \leq \frac{1}{2} \beta^{e-t} $$

# Operaciones de punto-flotante en máquina

Dado cualquier operación aritmética $\circ : \mathbb{R} \times \mathbb{R} \rightarrow \mathbb{R}$ en dos operandos en $\mathbb{R}$ ($\circ$ denota suma, resta, multiplicación o división), denotaremos por $\otimes$ la correspondiente operación de máquina.

$$ \otimes : \mathbb{R} \times \mathbb{R} \rightarrow \mathbb{F} \: , \quad \quad
x \otimes y = fl( fl(x) \circ fl(y)) $$


**La siguiente propiedad se cumple**: $\forall \, x , \, y \in \mathbb{F} \, , \exists \delta \in \mathbb{R}$ tal que
$$ x \otimes y = (x \circ y)(1 + \delta) \quad \quad \text{con} \: |\delta| \leq u $$
^ca8000

Para que la propiedad anterior propiedad se cumpla cuando $\circ$ es el operador de resta, se requerirá un supuesto adicional sobre la estructura de los números en $\mathbb{F}$, es decir, la presencia del llamado *dígito de redondeo*. En particular, cuando $\circ$ es el operador suma, se sigue que $\forall \: x \,, y \in \mathbb{F}$ 
$$ \frac{|x \oplus y - (x + y)|}{|x + y|} \leq u(1+u) \frac{|x| + |y|}{|x + y|} + u \: ,$$



de modo que el *error relativo* asociado con cada operación de máquina será pequeño, a menos que $x + y$ no sea pequeño por sí mismo. 


## Algunas reglas

### Suma/Resta en punto flotante
Sean $x, y \in \mathbb{F}(\beta, t, L, U)$. Luego $x \pm y$ se calcula como sigue:

1. **Alinear mantisas**. Tomar el número con menor exponente y desplazar su mantisa a la derecha hasta igualar los exponentes.
2. Sumar/Restar mantisas.
3. **Normalizar** el resultado si fuera necesario.
4. **Redondear** la mantisa al número de dígitos apropiado.
5. **Normalizar** si fuera preciso.

### Multiplicación/División en punto flotante
Sean $x, y \in \mathbb{F}(\beta, t, L, U)$. Luego $x \times y$, $x / y$, se calcula como sigue:

1. **Sumar/restar los exponentes**.
2. **Multiplicar/dividir mantisas**.
3. **Normalizar** el resultado.
4. **Redondear** la mantisa al número de dígitos apropiado.
5. **Normalizar** si es preciso.
6. **Determinar** el signo del resultado.




# Representación IEEE 754
Esta norma define dos formatos básicos de punto flotante con base $\beta = 2$. La
distribución de los N bits son en el siguiente orden:

| Formato precision | Palabra (N) | Signo (s) | Exponente sesgado (E) | Mantisa (m) |
| ----------------- | :---------: | :-------: | :-------------------: | :---------: |
| Simple            |     32      |     1     |           8           |     23      |
| Doble             |     64      |     1     |          11           |     52      |

## Precisión simple - IEEE 754
Considera el sistema de punto flotante $\mathbb{F}(2, 24,−126, 127)$ y una longitud de palabra igual a $N = 32$ bits. Dado $x \in \mathbb{R}$ en notación científica normalizada de la forma siguiente:
$$ x = (-1)^s (d_1 , d_2 ... d_{23}d_{24}d_{25}...)_2 \times 2^e, d_1 \neq 0 $$
su respectiva notación en punto flotante es:
$$ fl(x) = (-1)^s (d_1 . d_2d_3 ... d_{23}d_{24}) \times 2^e $$
Como en base 2 se cumple que $d_1 = 1$ siempre, entonces su representación en el computador es como sigue:
• Si tenemos n bits para el exponente, calculamos el sesgo como sigue $2^{n−1} − 1$. Para $n = 8$ el sesgo es $2^7 − 1 = 127$.
• Expresamos el exponente sesgado: $E = e + 127$ en base $2$.
• Colocamos los dígitos $d_2, d_3, . . . d_{24}$ en los bits asignados a la mantisa.
• El dígito $d_1$ es llamado **bit escondido**.

## Números especiales IEEE-754

- El **cero** es representado con ceros para el exponente y la mantisa
- Los valores $+\infty$ y $-\infty$ son representados con el máximo valor para el exponente ($2^n - 1)$ y $0$ para la mantisa
- Si el exponente toma el máximo valor y la mantisa es **no nula** se tiene la ocurrencia de **NaN**, que representa expresiones como: $0 \times \infty$,  $0 / 0$ , $\infty / \infty$, $\infty - \infty$



## Precisión doble - IEEE 754
Considera el sistema de punto flotante $\mathbb{F}(2, 53,−1022, 1023)$ y una longitud de palabra igual a $N = 64$ bits. Dado $x \in \mathbb{R}$ en notación científica normalizada de la forma siguiente:
$$ x = (-1)^s (d_1 , d_2 ... d_{53}d_{54}d_{55}...)_2 \times 2^e, d_1 \neq 0 $$
su respectiva notación en punto flotante es:
$$ fl(x) = (-1)^s (d_1 . d_2d_3 ... d_{53}d_{54}) \times 2^e $$
Como en base 2 se cumple que $d_1 = 1$ siempre, entonces su representación en el computador es como sigue:
• Si tenemos n bits para el exponente, calculamos el sesgo como sigue $2^{n−1} − 1$. Para $n = 10$ el sesgo es $2^{10} − 1 = 1023$.
• Expresamos el exponente sesgado: $E = e + 1023$ en base $2$.
• Colocamos los dígitos $d_2, d_3, . . . d_{54}$ en los bits asignados a la mantisa.
• El dígito $d_1$ es llamado **bit escondido**.



## Cancellation errors
**Para el caso de la suma de dos número cercanos en módulo, pero opuestos en signo. De hecho, en tal caso $x+y$ puede ser bastante pequeño, esto genera los llamados errores de cancelación. 


## Flops
Es importante notar que junto con las propiedades de la aritmética estándar que se preservan cuando se pasa a aritmética de punto-flotante (por ejemplo, la conmutatividad de la suma para dos sumandos o el producto de dos factores), otras propiedades se pierden. **Por ejemplo, la propiedad asociativa de la suma**
$$ x \oplus (y \oplus z) \neq ( x \oplus y) \oplus z \: . $$

Denotaremos como *flop* la operación flotante elemental única (suma, resta, multiplicación, división) (se advierte al lector que en algunos textos *flop* identifica una operación de la forma $a + b \cdot c$ ). De acuerdo con la convención anterior, 

- el producto escalar entre dos vectores de longitud n requerirá $2n+1$ *flops*, 
$$ 
\begin{array}{cc} 
(a_1, a_2, ... , a_n) \cdot (b_1, b_2, ... , b_n) \\
\\ 
\left. \begin{array}{c}
c_1 = a_1b_1 \: , \quad 1 \\
c_2 = a_2b_2 \: , \quad 2 \\
. \\ . \\ . \\
c_n = a_nb_n \: , \quad n \\ 
\end{array} \right\}
\text{n flops}

\begin{array}{l}
\quad \quad 1 \quad \underbrace{c_1 + c_2}_{} \\
\quad \quad 2 \quad \quad \underbrace{c_{12} + c_3}_{} \\
\quad \quad 3 \quad \quad \quad \underbrace{c_{123} + c_4}_{} \\
\quad \quad  . \\ \quad \quad . \\ \quad \quad . \\
\quad \quad n-1 \quad \underbrace{c_{123...(n-1)} + c_n}_{} \\
\end{array} \\
Por tanto, < \overline{u} , \overline{v} > \: \text{equivale a} \: 2n-1 \: \text{flops}
\end{array}$$

- un producto matrix-vector $(2n-1)m$ *flops* si la matriz es $m \times n$ y finalmente
- un producto matrix-matrix $(2r-1)mn$ *flops* si las dos matrices son de tamaño $m \times r$ y $r \times n$ respectivamente


## Exceptional situations
En la siguiente tabla informamos los resultados que se obtienen en situaciones excepcionales. La presencia de un $NaN$ (*not a number*) en una secuencia de operaciones implica automáticamente que el resultado es un $NaN$.
$$ \begin{array}{ccc} \hline
exception & examples & result \\ \hline
\text{non valid operation} & 0/0 \, , \: 0 \cdot \infty & NaN \\
overflow & & \pm \infty \\
\text{division by zero} & 1/0 & \pm \infty \\
underflow & & \text{subnormal numbers} \\ \hline
\end{array}$$

## Round digits
Mencionamos que no todos los sistemas de punto flotante satisfacen la [[#^ca8000|expresión]] líneas arriba. Una de las principales razones es la ausencia del dígito de redondeo en la resta, es decir, un bit adicional que entra en acción a nivel de la mantisa cuando se realiza la resta entre dos números de punto flotante. Para demostrar la importancia del dígito de redondeo, consideremos el siguiente ejemplo con un sistema $\mathbb{F}$ que tiene $\beta = 10$ y $t = 2$. Restemos $1$ y $0.99$. Tenemos


<div style="text-align: center;">
	<figure>
    <img src="C:\Users\mitch\OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA\Mi unidad\My Notes\My Notes\Analisis y Modelamiento Numerico\imgs\ejemplo redondeo digitos.png">
    <figcaption></figcaption>
    </figure>
</div>


$$ fl(x \pm y) = (x \pm y) (1 + \delta) \quad \text{con} \quad |\delta| \leq u \, ,$$
pero si la siguiente
$$ fl(x \pm y) = x(1 + \alpha) \pm y(1 + \beta) \quad \text{con} \quad |\alpha| + |\beta| \leq u \, .$$
Una aritmética en la que ocurre este último evento se denomina aberrante. En algunas computadoras, el dígito de redondeo no existe, y la mayor parte del cuidado se dedica a la velocidad en la computación. Sin embargo, hoy en día la tendencia es usar incluso dos dígitos de redondeo


# Notación científica normalizada

El punto decimal esta desplazado hacia la izquierda, es decir, todos los dígitos están a la derecha del punto decimal y el primer dígito no es $0$. Ejemplos:
- $732.5051 = 0.7325051 \times 10^3$
- $-0.005612 = -0.5612 \times 10^{-2}$

En general
$$ x = \pm r \times 10^n$$
donde $r$ es un número en el rango $\frac{1}{10} \leq r \leq 1$ y $n$ es un entero. 

A su vez, en notación científica para el sistema binario:
$$ x = \pm q \times 2^m$$
donde $q$ es un número en el rango $\frac{1}{2} \leq r \leq 1$ y $m$ es un entero. A $q$ se le denomina *mantisa* y al entero $m$ *exponente*. Ambos están en base $2$.

## Almacenando números binarios en la computadora
Supongamos que el dígito binario principal 1 se desplaza justo a la izquierda del punto binario. En este caso, la representación sería $q = (1.f)_2$ y $1 \leq q < 2$. Ahora solo $(.f)_2$ es almacenado en una palabra ahorrando 1 bit de espacio no almacenando el bit $1$ principal pero asumiendo que se encuentra allí. 

En una computadora, el almacenamiento en precisión simple para un número real en su representación en punto-flotante se divide en tres campos. Estos representan un número real diferente de 0, $x = \pm q \times 2^m$
- Signo de $x$: 1 bit
- Exponente con bias (e): 8 bits
- Mantisa (número real $f$): 23 bits

Un número real $x = \pm q \times 2^m$ se puede escribir como un número binario normalizado desplazado hacia la izquierda de modo que el primer bit distinto de cero en la mantisa esté justo antes del punto binario, esto es, $q = (1.f)_2$. Este bit puede ser asumido como $1$ y no requiere almacenamiento. La mantisa esta en el rango $1 \leq q < 2$. **Los 23 bits reservados en la palabra para la mantisa se pueden utilizar para almacenar los 23 bits de f**. Entonces, en efecto, la maquina tiene una mantisa de 24 bits para números de punto flotante.

# Nearby Machine Numbers
Ahora queremos evaluar el error involucrado al aproximar un número real positivo dado $x$ por un número de máquina cercano en una computadora de 32 bits. Suponemos que:
$$ x = q \times 2^m ,\quad 1 \leq q < 2 ,\quad -126 \leq m \leq 127$$
Nos preguntamos, cual es el número de máquina más cercano a $x$. Tenemos que
$$ x = (1.a_1a_2 ... a_{23}a_{24}a_{25} ...)_2 \times 2^m$$
donde $a_i = 0, 1$. Un número de maquina cercano se obtiene simplemente desechando los bits en exceso $a_{24}a_{25}...$. A este proceso se le llama *truncamiento*. El número resultante es
	$$ x\_ = (1.a_1a_2 ... a_{23})_2 \times 2^m$$
Observe que $x\_$ se encuentra a la izquierda de $x$ en la recta real. Otro número de máquina cercano se encuentra a la derecha de $x$. Se obtiene *redondeando hacia arriba*, es decir, eliminamos los bits en excesos pero aumentamos en una unidad el ultimo bit $a_{23}$. Este número es
$$ x_+ = ((1.a_1a_2 ... a_{23})_2 + 2^{-23}) \times 2^m$$


# Diferencia cancelativa
Sean dos números de 6 dígitos de precisión, $x = 0.467546$, e $y = 0.462301$, que podemos representar solo con cuatro dígitos como $fl(x) = 0.4675$, y $fl(y) = 0.4623$, y que al ser restados nos dan $fl(x − y) = 0.0052$. Como vemos aunque el resultado es exacto para la suma de los números flotantes, de cuatro dígitos de precisión, no así con respecto a los números originales, que tenían seis dígitos. De hecho el resultado ha perdido dígitos, sólo tiene dos dígitos de precisión, cuando los operandos tenían cuatro. Este fenómeno de pérdida de dígitos de precisión se denomina cancelación, o **diferencia cancelativa**, y puede ser peligroso (*cancelación catastrófica*) si el resultado de la resta es utilizado posteriormente en otras operaciones, pues para ellas, uno de los operandos tiene solo dos dígitos de precisión.


# Error absoluto y relatico y pérdida de significancia
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


