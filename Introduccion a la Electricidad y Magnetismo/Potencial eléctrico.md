# Diferencia de potencial
Al igual que la fuerza gravitatoria, la fuerza eléctrica es conservativa. Existe por tanto una función energía potencial $U$ asociada con la fuerza eléctrica. La variación de la función energía potencial $dU$ viene definida por
$$ dU = - \vec{F} \cdot d \vec{l} $$
La fuerza ejercida por un campo eléctrico $\vec{E}$ sobre una carga puntual $q$ es $\vec{F} = q\vec{E}$, cuando la carga experimenta un desplazamiento $d\vec{l}$, en un campo eléctrico $\vec{E}$, la variación de energía potencial electrostática es
$$ dU = -q \vec{E} \cdot d\vec{l} $$
## Diferencia de potencial
La variación de energía potencial por unidad de carga se denomina **diferencia de potencial** $dV$
$$ dV = \frac{dU}{q} = - \vec{E} \cdot d\vec{l} $$

## Diferencia de potencial finita
Para un desplazamiento finito desde el punto $a$ hasta el punto $b$, el cambio de potencial es
$$ \Delta V = V_b - V_a = \frac{\Delta U}{q} = - \int_a^b  \vec{E} \cdot d\vec{l} $$
La diferencia de potencial $V_b - V_a$ es el valor **negativo** del trabajo por unidad de carga realizado por el campo eléctrico sobre una carga de prueba positiva cuando esta se desplaza del punto $a$ al punto $b$, para ello **Las posiciones del resto de cargas deben permanecer invariables**.

Del mismo modo que en la energía potencial $U$, solo tiene importancia el cambio de potencial $V$. Tenemos la libertad de elegir el potencial de tal modo que sea cero en el punto que más nos convenga. Si el potencial eléctrico y la energía potencial de una carga testigo se eligen de modo que sean iguales a cero en el mismo punto, ambas magnitudes son iguales y están relacionadas por

## Relación entre la energía potencial $U$ y potencial $V$
$$  U = qV $$
para una carga de prueba $q$.

## Continuidad de V
La función potencial es continua en todos los puntos del espacio, **excepto en aquellos puntos en los que el campo eléctrico es infinito**.

## Unidades
El potencial eléctrico es la energía potencial electrostática 
La unidad para el potencial **volt (V)** 
$$1 V = 1 \: J / C $$
$$ 1 \: N/C = 1 \: V/m $$

Un **electronvolt (eV)** equivale a $1 eV = 1.602 \times 10^{-19} J$

## Potencial y líneas de campo eléctrico
La energía potencial eléctrica $U$ se relaciona con el potencial eléctrico $V$ mediante la expresión $U = qV$ de forma que para una *carga positiva* la región del espacio en la que existe menor energía potencial es también la región en la que existe menor potencial eléctrico. Una carga positiva se acelera en la dirección de $\vec{E}$ y se dirige a zonas de más bajo potencial eléctrico.

>Las líneas de campo eléctrico $\vec{E}$ señalan en la dirección en la que el potencial eléctrico 
disminuye más rápidamente.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Potencial y lineas de campo.png" alt="">
    <figcaption>Pontencial y líneas de campo eléctrico</figcaption>
    </figure>
</div>

# Potencial debido a un sistema de cargas puntuales

El potencial eléctrico a una distancia $r$ de una carga puntual $q$ situada en el origen puede calculares como
>$$ V_p - V_{ref} = - \int_{ref}^p \vec{E} \cdot d \vec{l} $$

donde el punto de referencia tiene un potencial $V_{ref}$ y $P$ es el punto arbitrario en el que se calcula el potencial.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Potencial en un punto.png" alt="">
    <figcaption>Potencial en un cualquiera dado un punto de referencia</figcaption>
    </figure>
</div>

tenemos que
$$  V_p - V_{ref} = - \int_{ref}^p \vec{E} \cdot d \vec{l} = - \int_{ref}^p \frac{kq}{r^2} \hat{r} \cdot d \vec{l} = - \int_{ref}^{r_p} \frac{kq}{r^2} dr   $$
El punto de referencia se elige de tal forma que  $V_{ref} = 0$, entonces
$$   V_p - 0 = - \int_{ref}^p \vec{E} \cdot d \vec{l} = - kq \int_{ref}^{r_p} \frac{1}{r^2} dr = kq \left(\frac{1}{r_p} - \frac{1}{r_{ref}} \right) $$
$$ V_p =  kq \left(\frac{1}{r_p} - \frac{1}{r_{ref}} \right) $$
Como el punto de referencia es arbitrario, tomamos como el punto más lejano a la carga puntual $r_{ref} \to \infty$ y tenemos

## Potencial de Coulomb
> $$ V = \frac{kq}{r_p} $$

donde $r_p$ es la distancia desde el origen al punto donde consideramos el potencial.

## Energía potencial electrostática de un sistema de dos cargas
La energía potencial $U$ de una carga de prueba $q'$ situada a una distancia $r$ de la carga puntual $q$ es
$$ U = q'V = q\left(\frac{kq}{r}\right) = \frac{kq'q}{r} $$
donde $U = 0$ a una distancia infinita.

Alternativamente **el trabajo que debemos hacer en contra del campo eléctrico para llevar una carga de prueba $q'$ desde una gran distancia hasta la distancia $r$ de $q$ es** $$\frac{kq'q}{r}$$
El trabajo por unidad de carga es $kq/r$, que es el potencial en el punto $P$ referido al potencial cero del infinito.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Trabajo y potencial electrico.png" alt="">
    <figcaption>Trabajo y potencial eléctrico</figcaption>
    </figure>
</div>

## Potencial debido a un sistema de cargas puntuales
Es igual a la suma de los potenciales debidos a cada carga por separado. 
$$ V_p = \sum_{i=1}^{n} \frac{kq_i}{r_i} $$
donde $r_i$ es la distancia desde la carga $i$ al punto $P$ donde deseamos calcular el potencial.



# Determinación del campo eléctrico a partir del potencial 

Consideremos un pequeño desplazamiento $d\vec{l}$ en un campo electrostático arbitrario $\vec{E}$. La variación del potencial eléctrico viene dado por $-\vec{E} \cdot d\vec{l}$. Si el desplazamiento es perpendicular a $\vec{E}$ el potencial no cambia. Para un determinado valor de $|d\vec{l}|$ el máximo crecimiento de V se produce cuando el desplazamiento es en el sentido contrario a $\vec{E}$.

$$ dV = -\vec{E} \cdot d\vec{l} = -Ecos\theta dl = E_{tan} dl$$
donde $E_{tan} = Ecos\theta$ es la componente (tangencial) en la dirección de $d\vec{l}$, por tanto se tiene que
$$ E_{tan} = - \frac{dV}{dl} $$
Para un $d\vec{l}$ dado, el mayor incremento de $V$ se produce cuando el desplazamiento $d\vec{l}$ esta dirigido a lo largo de $-\vec{E}$. Un vector que señala en la dirección de la máxima variación de una función escalar y cuyo módulo es igual a la derivada de la función con respecto a la distancia en dicha dirección se denomina **gradiente** de la función. 

Si el potencial $V$ solo depende de $x$, para un desplazamiento en la dirección $x$, $d\vec{l} = dx \hat{i}$ y 
$$ dV(x) = -\vec{E} \cdot d\vec{l} = - \vec{E} \cdot dx \hat{i} = -E_x dx$$
por tanto 
$$ E_x = \frac{dV(x)}{dx} $$
para una distribución de carga esféricamente simétrica, el potencial puede ser una función exclusiva de la distancia radial y
$$ \vec{E}_r = - \frac{dV(r)}{dr}$$
En general
$$E_{x_i} = - \frac{\partial V(x_i)}{\partial x_i}$$
## Relación general entre $\vec{E}$ y $V$
El gradiente de $V$ se denota por $\nabla V$, por tanto

>$$  \vec{E} = - \nabla V $$
# Calculo de V para distribuciones continuas de carga

## Potencial debido a una distribución de carga continua
Se elige un elemento de carga $dq$ que pueda considerarse como una carga puntual y tomando en consideración el principio de superposición, el potencial se obtiene convirtiendo la suma en la [[#Potencial debido a un sistema de cargas puntuales#Potencial debido a un sistema de cargas puntuales|ecuación]] en la siguiente integral

$$ V = \int \frac{kdq}{r} $$
Donde suponemos que $V = 0$ a una distancia infinita.

## Potencial $V$ en el eje de un anillo cargado

Sea un anillo uniformemente cargado de radio $a$ uniformemente cargado de carga $Q$.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/potencial-eje-anillo.png" alt="">
    <figcaption>Potencial en el eje de un anillo</figcaption>
    </figure>
</div>
La distancia del punto $P$ en el eje a un elemento de carga $dq$ es $\sqrt{z^2 + a^2}$, entonces el potencial en $P$ debido al anillo es

$$ 
\begin{aligned}
V &= \int \frac{kdq}{r} = \int \frac{kdq}{\sqrt{z^2 + a^2}} = \frac{kQ}{\sqrt{z^2 + a^2}} \\
V &= \frac{kQ}{\sqrt{z^2 + a^2}}
\end{aligned}
$$



## Potencial $V$ en el eje de un disco uniformemente cargado

Sea un disco de radio $R$ que posee una carga total $Q$ distribuida uniformemente sobre su superficie
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/potencial-eje-disco.png" alt="">
    <figcaption>Potencial en el eje de un disco</figcaption>
    </figure>
</div>

Hallaremos el potencial en el disco como suma de potenciales de anillos de radio $a$ y anchura $da$. Tenemos que $dq = \sigma dA = \sigma 2 \pi a da$, donde $\sigma$ es la densidad superficial de carga. Integrando en $a$ de $0$ a $R$ se tiene

$$
V = \int \frac{kdq}{r} = \int \frac{kdq}{\sqrt{z^2 + a^2}} = \int \frac{k\sigma 2 \pi a }{\sqrt{z^2 + a^2}}da
$$
$$
V =  k\sigma 2 \pi \left( \sqrt{z^2 + a^2}  - \sqrt{z^2}\right)
$$
$$
V =  2 \pi  k\sigma |z| \left( \sqrt{1 + \frac{R^2}{z^2}}  - 1\right)
$$


## Potencial $V$ debido a un plano infinito de carga
La anterior [[#Calculo de V para distribuciones continuas de carga#Potencial $V$ en el eje de un disco uniformemente cargado|ecuación]] no es válida para un disco uniformemente cargado de radio infinito, ya que se supuso que $V=0$ en el infinito. Para distribuciones de carga que se extienden hasta el infinito debemos elegir $V=0$ en algún punto finito.

![[Pasted image 20240509153337.png]]

$$ V = V_0 - 2 \pi k \sigma |x| $$


## Potencial $V$ en el interior y en el exterior de una corteza esférica cargada
Dada una corteza esférica de radio $R$ y carga $Q$ distribuida uniformemente en su superficie.
Fuera de la corteza esférica, el campo eléctrico es radial y es el mismo que si toda la carga $Q$ fuera puntual y localizada en el origen
$$ \vec{E} = \frac{KQ}{r^2}\hat{r} $$
La variación del potencial correspondiente a un desplazamiento $d\vec{l}$ que tiene lugar fuera de la corteza es, por tanto,
![[Pasted image 20240509154711.png]]
En cualquier punto del volumen encerrado por la corteza esférica, el campo eléctrico es cero, entonces
![[Pasted image 20240509154630.png]]
donde $P$ es un punto arbitrario dentro del radio de la esfera. Dentro de la corteza el potencial es constante y es igual al trabajo necesario por unidad de carga para transportar una carga de prueba **desde el infinito hasta la corteza**.

Tenemos por lo tanto

$$
\left\{
\begin{array}{2}
\dfrac{kQ}{r} & (r \geq R) \\
\dfrac{kQ}{R} & (r \leq R)
\end{array}
\right.
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Grafica V vs r corteza-esferica.png" alt="">
    <figcaption>Grafica V vs r para una corteza esférica</figcaption>
    </figure>
</div>

### Observación
Una  región en la que el campo eléctrico es cero implica que el potencial es constante en todos sus puntos.

## Potencial $V$ generado por una esfera cargada uniformemente
Sea una esfera cargada de radio $R$ y carga $Q$ distribuida uniformemente. El campo eléctrico dentro de una esfera viene dado por $E_r = k\dfrac{Q}{R^3}r$. Fuera de la esfera, la carga se comporta como si fuera puntual, de modo que el potencial es $V = kQ/R$.

Dentro de la esfera, sabemos que el campo es $E_r = k\dfrac{Q}{R^3}r$ por la [[Distribuciones continuas de carga y Ley de Gauss#$ vec{E}$ debido a una esfera sólida uniformemente cargada|ecuación]] anteriormente hallada, entonces

$$
\begin{aligned}
V_p &= - \int_{\infty}^{r_p} E_rdr = -\int_{\infty}^{R} \frac{kQ}{r^2}dr -\int_{R}^{r_p} \frac{kQ}{R^3}rdr \\
&= \frac{kQ}{R} - \frac{kQ}{2R^3}(r_p^2 - R^2) \\
V_p &= \frac{kQ}{2R}(3-\frac{r_p^2}{R^2})
\end{aligned}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Grafica V vs r esfera-solida.png" alt="">
    <figcaption>Grafica V vs r para una esfera sólida</figcaption>
    </figure>
</div>



## Potencial $V$ debido a una carga lineal infinita
Sea una distribución de carga lineal infinita de densidad $\lambda$. 
El campo eléctrico viene dado por la [[Distribuciones continuas de carga y Ley de Gauss#Campo creado por una línea cargada|ecuación]] $\vec{E} = (2k\lambda/R)\hat{R}$.
La variación del potencial para un desplazamiento arbitrario $d\vec{l}$ viene dado por
$$ dV = -\vec{E} \cdot d\vec{l} = -\frac{2k\lambda}{R}\hat{R} \cdot d\vec{l} = -\frac{2k\lambda}{R} dR$$
Integrando desde un punto de referencia arbitrario hasta el punto $P$.
$$ 
\begin{aligned}
V_p - V_{ref} &= -2k\lambda \int_{R_{ref}}^{R_p} \frac{dR}{R} \\
\\
V_p - V_{ref} &= - 2k\lambda ln\frac{R_p}{R_{ref}}
\end{aligned}
$$
Se elige un punto de referencia en el que $V_{ref} = 0$, sin embargo este no puede ser $R_{ref} = 0$ o $R_{ref} = \infty$ por el logaritmo. Se debe elegir un punto dentro de ese intervalo.

$$ V = 2k \lambda ln \frac{R_{ref}}{R} $$
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Potencial linea-infinita.png" alt="">
    <figcaption>Potencial para una carga lineal infinita</figcaption>
    </figure>
</div>




# Superficies equipotenciales

## Ruptura dieléctrica
Muchos materiales no conductores se ionizan en campos eléctricos muy altos y se convierten en conductores. Este fenómeno, llamado **ruptura eléctrica** tiene lugar cuando la intensidad del campo eléctrica es $E_{max} = 3 \times 10^6 V / m = 3 \, MN / C$.

La intensidad del campo eléctrico para el cual tiene lugar la ruptura dieléctrica de un material se denomina **resistencia dieléctrica** de dicho material. Para el aire vale aproximadamente $3 \, MV / m$.

# Energía potencial electrostática
Los objetos que se repelen tienen mayor energía potencial cuanto menor es la distancia entre ellos, y si se atraen es mayor su energía potencial cuanto mayor es la distancia entre ellos.

## Energía potencial electrostática de un sistema de cargas puntuales

>La energía potencial electrostática de un sistema de cargas puntuales es el trabajo necesario para transportar las cargas desde una distancia infinita hasta sus posiciones finales

La energía potencial electrostática $U$ de un sistema de $n$ cargas puntuales se calcula como
>$$ U = \frac{1}{2} \sum_{i=1}^n  q_i V_i $$

donde $V_i$ es el potencial en la posición de la carga $i$ producido por todas las demás cargas.

Consideremos un  conductor esférico de radio $R$. Cuando la esfera contiene una carga $q$, su potencial relativo a $V=0$ en el infinito es 
$$ V = \frac{kq}{R} $$
El trabajo necesario para transportar una cantidad adicional de carga $dq$ desde el infinito al conductor es $Vdq$. Este trabajo es igual al incremento de la energía potencial del conductor:
$$ dU = Vdq = \frac{kq}{R}dq $$
La energía potencial total $U$ es la integral de $dU$ cuando $q$ crece desde cero hasta su valor final $Q$. Integrando, se obtiene
$$ U = \frac{k}{R} \int^{Q}_0 qdq = \frac{kQ^2}{2R} = \frac{1}{2} QV $$
donde $V = kQ/R$ es el potencial generado en la superficie de la esfera cargada.
## Energía potencial electrostática de un sistema de conductores
$$ U = \frac{1}{2} \sum_{i=1}^n  Q_i V_i $$

