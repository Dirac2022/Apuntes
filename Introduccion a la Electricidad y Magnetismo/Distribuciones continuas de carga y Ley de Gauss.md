

$$ d\vec{F} = dq \vec{E} $$
# Campo eléctrico $\vec{E}$ mediante la ley de Coulomb


El campo eléctrico $d\vec{E}$ en un punto del campo $P$ debido a este elemento de carga viene dado por la ley de Coulomb

$$
d\vec{E} = dE_r\vec{r} = \frac{kdq}{r^2}\vec{r}
$$
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Diferencial de carga.png" alt="">
    <figcaption>Diferencial de carga</figcaption>
    </figure>
</div>


## Campo eléctrico debido a una distribución continua de carga

$$ d\vec{E} = \frac{kdq}{r^2}\hat{r} \rightarrow \vec{E} = k \int \frac{\hat{r}}{r^2} dq = k\int \frac{\vec{r}}{r^3} dq $$
donde  $k  = \frac{1}{4\pi \varepsilon_0}$

## Distribución de carga uniforme

-  Volumétrico : $$\rho =\frac{Q}{V} C/ m^3$$ $$ dq = \rho dV \quad Q = \int \rho dV $$
- Superficial : $$\sigma =\frac{Q}{S} C/ m^2$$ $$ dq = \sigma dA \quad Q = \int \sigma dA $$
- Lineal: $$\lambda =\frac{Q}{L} C/ m$$  $$ dq = \lambda dl \quad Q = \int \lambda dl $$



## Campo creado por una línea cargada 
### En el punto medio
![[Pasted image 20240412094942.png]]


De longitud $L$ tal que $\lambda = \frac{Q}{L}$

$$\vec{E} = k \int \frac{\vec{r}}{r^3} dq \quad dq = \lambda dx$$
Donde $\vec{r} = y\hat{j} - x\hat{i}$. Por simetría
$$E_x = 0$$
y

$$E_y = k\lambda \int_{-L/2}^{L/2} \frac{dx}{(x^2 + y^2)^{3/2}}$$
$$ E_y = \frac{k\lambda}{y} \frac{L}{\sqrt{(\frac{L}{2})^2 + y^2}} $$
$$ E_y = \frac{k}{y} \frac{Q}{\sqrt{(\frac{L}{2})^2 + y^2}} $$

### General
El campo eléctrico debido a una línea uniforme cargada que se extiende hasta el infinito en ambas direcciones viene dado por 
$$ 
\begin{aligned}
\vec{E} &= \frac{2k\lambda}{R} \hat{R} \\ \\
	\vec{E} &= \frac{\lambda}{2\pi \varepsilon_0 R} \hat{R}
\end{aligned}
$$
donde $\lambda$ es la densidad lineal de carga, $R$ es la distancia radial de la línea de carga al punto de campo y $\hat{R}$ es el vector unitario en la dirección radial.
## Campo en el eje de un anillo

![[Pasted image 20240412095007.png]]

$$  \vec{E} = k \int \frac{\vec{r}}{r^3} dq $$
$$ \vec{r} = x \hat{i} + a \hat{e}_{\perp} $$
$$ \vec{E} = \vec{E_x} + \vec{E_{\hat{e}_{\perp}}} $$
Por simetría $\vec{E_{\hat{e}_{\perp}}} = 0$ y nos queda

$$ \vec{E} = \vec{E_x} = k \int_{0}^{2\pi} \frac{x}{r^3} \lambda a d \phi $$
$$ \vec{E} = k Q \frac{x}{(x^2 + a^2)^{3/2}} $$


## Campo en el eje de un disco

![[Pasted image 20240412101619.png]]
Sumaremos los campos creados por los anillos de radio $a$
Sabemos que $dq = \sigma dS = \sigma2\pi a da$, es decir el diferencial de carga en toda la longitud de nuestro "anillo", entonces, nuestro diferencial de campo dada una "porción de área" por el "anillo"
$$ dE_x = k\frac{xdq}{(x^2 + a^2)^{3/2}} $$
$$ E_x = k \int \frac{x\sigma2\pi a da}{{(x^2 + a^2)^{3/2}}} $$
$$ E_x = k \sigma\pi x \int \frac{2ada}{{(x^2 + a^2)^{3/2}}} $$

$$ E_x = k \pi \sigma x \left[ -2(x^2 + a^2)^{-1/2}\right]^R_0 $$
$$ E_x = \frac{2\pi\sigma kx}{|x|} \left( 1 - \frac{1}{\sqrt{1 + \frac{R^2}{x^2}}}
\right) $$
$$ E_x = 2\pi\sigma k sign(x) \left( 1 - \frac{1}{\sqrt{1 + \frac{R^2}{x^2}}}
\right) $$
## Campo creado por un plano infinito
Si el radio del "disco" es $R$ y $R \to \infty$ , tenemos
$$ 
\begin{aligned}
E_x &= 2\pi k \sigma sign(x) \\ \\
E_x &= \frac{\sigma}{2\varepsilon_0}(sing(x))
\end{aligned}
$$


### Campo creado entre dos planos infinitos con cargas opuestas
- **Fuera de los planos la carga es cero**
- **Dentro de los planos la carga es** $4\pi k \sigma$



# Ley de Gauss
Una superficie cerrada es aquella que divide el espacio en dos regiones diferentes, una interior y una exterior a una superficie.

> El número neto de líneas que sale por cualquier superficie que encierra las cargas es proporcional a la carga encerrada dentro de dicha superficie. Este es un enunciado cualitativo de la Ley de Gauss.

## Flujo eléctrico ($\phi$)
Se define como el producto del módulo del campo eléctrico $E$ y el área $A$.
$$ \phi = EA \quad N \cdot m^2 / C $$
siempre que la superficie $A$ sea perpendicular al campo eléctrico $E$, de lo contrario el flujo a través de una superficie viene definido por
$$ \phi = \vec{E} \cdot \vec{n} A = EAcos(\theta) $$
donde $\vec{E} \cdot \vec{n}$ es la componente de $\vec{E}$ normal a la superficie $A$, $\vec{n}$ es el vector unitario perpendicular a la superficie $A$.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/superficie-arbitraria.png" alt="">
    <figcaption>Flujo eléctrico en una superficie arbitraria</figcaption>
    </figure>
</div>
Si la superficie es arbitraria, se puede considerar para un $\Delta A_i$ como un plano, y la variación del campo eléctrico a través del elemento puede despreciarse, entonces el flujo del campo eléctrico a través de este elemento es
$$ \Delta \phi_i = \vec{E}_i \cdot \hat{n}_i \Delta A_i $$
El flujo total al través del a superficie es la suma de $\Delta \phi_i$. En el límite, cuando el número de elementos se aproxima a infinito y el área de cada elemento tiene a cero la suma se convierte en una integral. La definición de flujo eléctrico es por tanto

$$ \phi = \int_S \vec{E} \cdot \vec{n} dA $$
El signo del flujo depende de la elección que hagamos de la dirección del vector unitario perpendicular al elemento de superficie $\hat{n}$. Eligiendo $\hat{n}$ dirigido hacia el exterior de la superficie, podemos determinar el signo de $\vec{E} \cdot \hat{n}$, así como el signo del flujo a través de la superficie.

### Flujo eléctrico para una superficie cerrada

$$ \phi_{neto} = \oint_S \vec{E} \cdot \vec{n} dA $$
El flujo total o neto $\phi_{neto}$ a través de la superficie cerrada es positivo o negativo dependiendo de que $\vec{E}$ esté dirigido predominante hacia fuera o hacia adentro de la superficie. En los puntos de la superficie en que $\vec{E}$ está dirigido hacia adentro, $E_n$ es negativo.


## Ley de Gauss
El flujo neto a través de cualquier superficie es igual a la carga neta dentro de la superficie dividida por $\varepsilon_0$
$$   \phi_{neto} = \oint_S \vec{E} \cdot \vec{n} dA = \frac{Q_{interior}}{\varepsilon_0}
$$
donde $\varepsilon_0 = 8.854 \times 10^{-12} C^2 / (Nm^2)$.
La Ley de Gauss es válida para todas las superficies y distribuciones de carga.


# Cálculo del campo eléctrico $\vec{E}$ con la Ley de Gauss utilizando la simetría

Existen tres casos de simetría donde se puede calcular la Ley de Gauss
- **Simetría cilíndrica o lineal**, si la densidad de carga depende solo de la distancia a la línea.
- **Simetría planar**, si la densidad de carga depende solo de la distancia desde un plano (si la densidad de carga es constante en un plano o tiene simetría en dicho plano).
- **Simetría esférica**, si la densidad de carga solo depende de la distancia a un punto.

## $\vec{E}$ debido a una lámina uniformemente cargada
Sea una lámina grande de plástico (infinita) uniformemente cargada, de grosor $2a$ que ocupa la región del espacio entre los planos $z=-a$ y $z=+a$. La carga por unidad de volumen es $\rho$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/superficie-gaussiana-plano infinito.png" alt="">
    <figcaption>Superficie gaussiana para el calculo de E debido a un plano infinito</figcaption>
    </figure>
</div>

**Consideraciones**
- Si $\rho > 0$, $\vec{E}$ apunta hacia afuera de plano $z=0$
- Si $\rho < 0$, $\vec{E}$ apunta hacia dentro de plano $z=0$
- En $z=0$ el campo es nulo.

$$
\vec{E} = E_z\hat{k} = 
\left\{ 
\begin{array}{2} 
- \dfrac{\rho a}{\epsilon_0} & (z \leq a) \\
\\
\dfrac{\rho z}{\epsilon_0} & (-a \leq z \leq a) \\
\\
\dfrac{\rho a}{\epsilon_0} & (z \geq a) \\
\end{array}
\right.
$$
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/grafica-E-plano infinito.png" alt="">
    <figcaption>Grafica E vs z para una lámina infinita de grosor 2a</figcaption>
    </figure>
</div>

## $\vec{E}$ debido a una corteza esférica cargada de grosor reducido
Se tiene una corteza esférica de radio $R$ y carga total $Q$
Como se presenta simetría esférica, se usa una superficie gaussiana esférica de radio $r$.
-  $\vec{E}$ presenta simetría radial
- Si $r<R$, entonces $Q_{interior} = 0$ 
- Si $r>R$, entonces $Q_{interior} = Q$

$$ \vec{E} = E_r \hat{r} $$
$$
E_r = 
\left\{
\begin{array}{2} 
\dfrac{1}{4\pi \epsilon_0} \dfrac{Q}{r^2} & r > R \\
\\
0 & r < R
\end{array}
\right.
$$

### Observación
Es preciso hacer notar que el campo eléctrico es discontinuo en $r=R$, donde la densidad de carga superficial es $\sigma = Q/(4\pi R^2)$. Justo fuera de la corteza el campo eléctrico es $E_r = \sigma / \epsilon_0$. Como el campo dentro de la corteza es cero **el campo eléctrico es discontinuo en $r=R$ con un salto cuyo valor es $\sigma / \epsilon_0$**.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/grafica Er vs r corteza-esferica.png" alt="">
    <figcaption>grafica Er vs r para una corteza esférica</figcaption>
    </figure>
</div>

## $\vec{E}$ debido a una esfera sólida uniformemente cargada
Sea una esfera sólida uniformemente cargada de radio $R$ y carga $Q$. Por simetría, el campo eléctrico debe ser radial. Se elige una superficie gaussiana esférica de radio $r$.
Se tiene que
$$  \vec{E} = E_r \hat{r}  $$
y

$$
E_r = 
\left\{
\begin{array}{2} 
\dfrac{1}{4\pi \epsilon_0} \dfrac{Q}{r^2} & r \geq R \\
\\
\dfrac{1}{4\pi \epsilon_0} \dfrac{Q}{R^3}r & r \leq R
\end{array}
\right.
$$
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/grafica Er vs r esfera-solida.png" alt="">
    <figcaption>grafica Er vs r para una esfera sólida</figcaption>
    </figure>
</div>
## $\vec{E}$ debido a una carga lineal infinita
Se tiene un campo eléctrico debido a una carga lineal infinitamente larga de densidad de carga uniforme $\lambda$.

**Consideraciones**:
- El campo apunta hacia afuera si $\lambda$ es positivo.
- El campo apunta hacia adentro si $\lambda$ es negativo.
- El módulo del campo eléctrico depende exclusivamente de la distancia radial del punto de observación a la línea cargada.
- Se elige como superficie gaussiana a un cilindro de longitud $L$ y radio $R$ cuyo eje sea la línea de carga.


$$   \vec{E} = E_R \hat{R} $$
y
$$ E_r = \dfrac{1}{2\pi \epsilon_0} \dfrac{\lambda}{R} $$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/superficie gaussiana para carga lineal infinita.png" alt="">
    <figcaption>Superficie gaussiana para un campo debido a una carga lineal infinita</figcaption>
    </figure>
</div>
### Observación
En las proximidades del extremo de una carga lineal de longitud **finita** no podemos suponer que $\vec{E}$ es perpendicular a la superficie cilíndrica o que $E_n$ es constante de todos los puntos de la misma, por tanto no puede utilizarse Gauss para hallar el campo eléctrico.


# Discontinuidad de $E_n$
El campo eléctrico correspondiente a un plano infinito, una corteza esférica o en general, para una componente del campo eléctrico perpendicular a una superficie de carga $\sigma$ presenta una discontinuidad en la cantidad
$$ \Delta E_n = \frac{\sigma}{\epsilon_0} $$
donde $\Delta E_n$ es la variación de campo eléctrico (en la componente normal) en ambas caras de la superficie.
La discontinuidad de $E_n$ ocurre tanto en un disco finito cargado como en un plano infinito o una corteza esférica con una distribución de carga superficial. **Esta discontinuidad no aparece en una superficie de distribución de carga volumétrica**. El campo eléctrico es discontinuo en **cualquier lugar donde haya una densidad de carga volúmica infinita** (la cantidad de carga por unidad de volumen es infinitamente grande) como densidades de carga lineal finita y densidades de carga superficial finita.

# Carga y campo en la superficie de los conductores
Mediante la Ley de Gauss se demuestra que toda **carga eléctrica neta** de un conductor reside en su superficie.
1. Sea una superficie gaussiana situada en el interior de la superficie real de un conductor en equilibrio electrostático. Como el campo eléctrico es cero en todos los puntos dentro del conductor, será también cero en todos los puntos de la superficie gaussiana.
2. Por tanto si existe una carga neta en el conductor, ésta debe residir sobre la superficie del propio conductor.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/superficie-gaussiana interior conductor.png" alt="">
    <figcaption>Superficie gaussiana en el interior de un conductor</figcaption>
    </figure>
</div>
En la superficie de un conductor en equilibrio, el campo eléctrico $\vec{E}$ debe ser perpendicular a la superficie, de lo contrario se produciría una aceleración tangencial a ella hasta que se anulara dicha componente.

El campo eléctrico en los puntos **fronterizos** con la superficie del conductor es
$$ E_n = \frac{\sigma}{\epsilon_0} $$
ya que $E_n$ es discontinuo en cualquier superficie en la cantidad $\sigma / \epsilon_0$ y es cero dentro del conductor.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Resumen1-Distribuciones-continuas-Gauss.png" alt="">
    <figcaption>Resumen 1</figcaption>
    </figure>
</div>
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Resumen2-Distribuciones-continuas-Gauss.png" alt="">
    <figcaption>Resumen 2</figcaption>
    </figure>
</div>
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Resumen3-Distribuciones-continuas-Gauss.png" alt="">
    <figcaption>Resumen 3</figcaption>
    </figure>
</div>


