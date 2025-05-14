# Problema 7

## Parte (a)
$A(10000, 4)$, $B(9000,5)$
Primero, encontramos la pendiente $m$ de la demanda.

$$
m = \frac{\Delta p}{\Delta q} = \frac{5 - 4}{9000 - 10000} = \frac{1}{-1000} = -\frac{1}{1000}
$$

La ecuación de la demanda en forma **punto-pendiente** es:

$$
p - p_1 = m(q - q_1)
$$

Usando el punto $(p_1, q_1) = (10000, 4)$:

$$
p - 4 = -\frac{1}{1000}(q - 10000)
$$

$$
p - 4 = -\frac{q}{1000} + 10
$$

$$
p = -\frac{1}{1000}q + 14
$$
## Parte (b)


$$
p = 
\begin{cases}
3.2 + \dfrac{q}{2000}, & \text{si } 0 \leq q \leq 6000 \\ \\
5 + \dfrac{q}{5000}, & \text{si } q \geq 6000
\end{cases}
$$


Si $0 \leq q \leq 6000$:

$$
3.2 + \frac{q}{2000} = -\frac{1}{1000}q + 14
$$

Multiplicamos ambos lados por 2000 
$$
6400 + q = -2q + 28000
$$
$$
3q = 21600 \implies q = 7200
$$

Sin embargo, $q = 7200$ no está en el rango $0 \leq q \leq 6000$,

Si $q \geq 6000$

$$
5 + \frac{q}{5000} = -\frac{1}{1000}q + 14
$$

Multiplicamos ambos lados por 5000:

$$
25000 + q = -5q + 70000
$$
$$
6q = 45000 \implies q = 7500
$$

>[!tip] Para hallar el precio de equilibrio, podemos reemplazar la cantidad de equilibrio ya sea en la ecuación de la oferta o la ecuación de la demanda.

El precio de equilibrio es:

$$
p = 5 + \frac{7500}{5000} = 5 + 1.5 = 6.5
$$

Precio y cantidad de equilibrio: $(7500, 6.5)$

# Problema 10

---
Discriminate de una ecuación cuadrática
Dada la ecuación: $ax^2 + bx + c = 0$

$$
\Delta = b^2 - 4ac
$$

>[!tip] Si $\Delta = 0$ significa que la solución de la ecuación cuadrática es única

---

Por simple inspección $a=2$, $b=1$.
Igualamos las dos ecuaciones:

$$
x^2 + 2 = mx + 1
$$

$$
x^2 - mx + 1 = 0 \tag{*}
$$

El discriminante debe ser cero:

$$
\Delta = m^2 - 4(1)(1) = 0 \implies m^2 = 4
$$


$m=2, m=-2$

Entonces, $m=-2$  por la gráfica de la recta $\mathcal{L}$
$$
\mathcal{L}: y=-2x+1
$$

Encontremos las raíces de (\*)

$$
\begin{align*}
x^2 + 2x + 1 &= 0 \\
(x+1)^2 &= 0
\end{align*}
$$
Por tanto $x=-1$ y $T=(-1, -2(-1)+1)=(-1,3)$


# Problema 11

Las raíces de la parabola $\mathcal{P}$ son $x_1=1$ y $x_2=9$
Por tanto

$$
\mathcal{P}: y=(x-1)(x-9)=x^2-10x+9
$$
## Hallando el vértice de la parabola

### Mediante cálculo 

Hallamos $\dfrac{dy}{dx}=0$

$$
\dfrac{dy}{dx} = 2x-10 = 0 \to x=5
$$

Entonces $V(5,-16)$

### Completando cuadrados

>[!tip] 
>Si la parábola tiene la forma: $$a(x-h)^2 +k$$ 
>Entonces $V(h,k)$ son las coordenadas del vértice de la parábola.

Completando cuadrados:
$$
\begin{align*}
x^2 - 10x + 9 \\
x^2 - 2(x)(5) + 25 - 25 + 9 \\
(x-5)^2 - 16
\end{align*}
$$
Vemos que $V(5, -16)$

### Usando fórmula
Si tenemos una parabola de la forma $ax^2 + bx + c$
El vértice de la parábola $V(h, k)$ se calcula como

$$
h=\dfrac{-b}{2a}
$$

El valor de $k$ se calcula reemplazando $x=h$ en la ecuación de la parábola
# Problema 14

>[!tip] Ecuación ordinaria de la circunferencia
>$$ \mathcal{C}: (x-h)^2 + (y-k)^2 = r^2 $$
>donde el centro es $C(h, k)$ y el radio es $r$


Hallemos las ecuaciones de las circunferencias
$$
\mathcal{C_1}: x^2 + y^2 = 100
$$

$$
\mathcal{C_2}: (x-20)^2 + (y-15)^2 = 225
$$

Resolvamos $\mathcal{C_1} = \mathcal{C_2}$

$$
\begin{align*}
x^2 + y^2 &=  (x-20)^2 + (y-15)^2 \\
100 &= x^2-40x+400 + y^2 - 30y + 225 \\
&\vdots \\
4x+3y &= 500
\end{align*}
$$

Tenemos que $y=\dfrac{50-4x}{3}$
Reemplazando en cualquiera de las ecuaciones de circunferencia

$$
x^2 + \left(\dfrac{50-4x}{3}\right)^2 = 100
$$
Donde $x=8$, $\to$ $y=6$
Entonces $T(8,6)$

>[!tip] Area de un triángulo dada las coordenadas de sus vertices
Sea el triángulo ABC cuyos vertices son $A(a_1, a_2)$, $B(b_1, b_2)$, $C(c_1, c_2)$
El área se halla como
$$
\mathbb{A} = \dfrac{1}{2}\begin{vmatrix} a_1 & a_2  \\ b_1 & b_2 \\ c_1 & c_2 \\ a_1 & a_2 \end{vmatrix}
$$


Usemos la fórmula con las coordenadas $B(0,10)$, $T(8,6)$, $C(20,15)$

$$
\mathbb{A} = \dfrac{1}{2}\begin{vmatrix} 0 & 10  \\ 8 & 6 \\ 20 & 15 \\ 0 & 10 \end{vmatrix}
$$
Resolviendo
$$
\begin{align*}
\mathcal{A} &= \dfrac{1}{2} \left[(0+120+200)-(80+120+0) \right] \\ \\
&= \dfrac{1}{2} (320 - 200) \\ \\
&= 60 \\
\end{align*}
$$


# Problema 15

**Hallemos las coordenadas de los puntos**

$A(0,a)$ y $B(b_1, b_2)$ son los puntos de intersección entre la parábola $\mathcal{P}$ y la recta $\mathcal{L}$.
Además $D(0,b_2)$

$$
-x^2 + 6x + 11 = -2x + 11
$$

Donde $x_1 = 0$ y $x_2 = 8$
- Para $x_1 \to y_1 = 11$. Por tanto $A(0,11)$
- Para $x_2 \to y_2 = -5$. Por tanto $B(8,-5)$
Y $D(0,-5)$

>[!tip] Centro de un segmento
>Dado dos puntos $N(n_1, n_2)$ y $Q(q_1, q_2)$ el punto centro $M$ del segmento $\overline{PQ}$
>$$
>M = \left(\dfrac{n_1 + q_1}{2}, \dfrac{n_2 + q_2}{2}\right)
>$$

Hallamos las coordenadas de $C$

$$
\begin{align*}
M &= \left(\dfrac{0 + 8}{2}, \dfrac{11 -5}{2}\right) \\ \\
M &= (4,3)
\end{align*}
$$



**Hallemos el área del triángulo**
$A(0,11)$ , $D(0, -5)$, $B(8, -5)$
$$
\mathbb{A} = \dfrac{1}{2}\begin{vmatrix} 0 & 11  \\ 0 & -5 \\ 8 & -5 \\ 0 & 11 \end{vmatrix}
$$

$$
\begin{align*}
\mathcal{A} &= \dfrac{1}{2} \left|(0+0+88)-(0-40+0) \right| \\ \\
&= \dfrac{1}{2} (88 + 40) \\ \\
&= 64 \\
\end{align*}
$$

**Hallemos el radio $R$ de la circunferencia**
>[!tip] Distancia entre dos puntos
>Sean los puntos $P_1(x_1, y_1)$ y $P_2(x_2, y_2)$
>$$
>\text{Distancia} = d(P_1, P_2) = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}
>$$

$$
R = \sqrt{(11 - 3)^2 + (0- 4)^2} = 4\sqrt{5}
$$
# Problema 19

$\mathcal{P}: y = x^2 + 2x - 1$ 

## Parte a

$$
x^2 + 2x - 1 = 4x + b
$$

Reorganizamos:

$$
x^2 - 2x - (1 + b) = 0
$$

Igualando el discriminante a cero

$$
\Delta = (-2)^2 - 4(1)(-1 - b) = 4 + 4(1 + b) = 4 + 4 + 4b = 8 + 4b = 0
$$

Por tanto:

$$
8 + 4b = 0 \implies b = -2
$$



## Parte b

Igualamos las dos ecuaciones:

$$
x^2 + 2x - 1 = -2x^2 + ax + 2
$$

Reorganizamos:

$$
3x^2 + (2 - a)x - 3 = 0
$$

Para que esta ecuación tenga una única solución, el discriminante debe ser cero:

$$
\Delta = (2 - a)^2 - 4(3)(-3) = (2 - a)^2 + 36 = 0
$$

Sin embargo, $(2 - a)^2 + 36$ es siempre positivo

>[!error] No hay solución

## Parte c

La ecuación de una recta que pasa por $(-1, 0)$ es:

$$
y = m(x + 1)
$$
Igualamos las dos ecuaciones:

$$
x^2 + 2x - 1 = m(x + 1)
$$

Reorganizamos:

$$
x^2 + (2 - m)x - (1 + m) = 0
$$

El discriminante debe ser cero:

$$
\Delta = (2 - m)^2 - 4(1)(-1 - m) = 4 - 4m + m^2 + 4 + 4m = m^2 + 8 = 0
$$

Sin embargo, $m^2 + 8$ es siempre positivo

>[!error] No hay solución



$$
\mathcal{P}: y=-\frac{18}{144}x^2 + 18
$$

Reemplazando


