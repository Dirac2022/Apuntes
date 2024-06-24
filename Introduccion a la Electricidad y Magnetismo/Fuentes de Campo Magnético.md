
# Campo magnético creado por cargas puntuales en movimiento

## Campo magnético creado por una carga puntual móvil
Cuando una carga puntual $q$ se mueve con velocidad $\vec{v}$, se produce un campo magnético $\vec{B}$ en el espacio dado por
>$$ \vec{B} = \frac{\mu_0}{4\pi} \frac{q\vec{v} \times \hat{r}}{r^2} $$

donde $\hat{r}$ es un vector unitario que apunta desde la carga $q$, que se mueve con velocidad $\vec{v}$, al punto del campo $P$. $\mu_0$ es una constante llamada **permeabilidad del espacio libre**.

### Permeabilidad del espacio libre
$$ \mu_0 = 4\pi \times 10^{-7} \, T \cdot m / A = 4\pi \times 10^{-7} \, N/A^2 $$
donde $1$ tesla equivale a $1 \, T = 1 \, N/A$.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo-magnetico- generado por una carga.png" alt="Induccion por conexión a tierra" width=400>
    <figcaption>Campo magnético generado por una carga en movimiento</figcaption>
    </figure>
</div>



# Campo magnético creado por corrientes eléctricas (Ley de Biot-Savart)

## Ley de Biot-Savart
En la ecuación anterior, podemos reemplazar el elemento $q\vec{v}$ por un elemento de corriente $Id\vec{l}$ , ya que $q\vec{v} = qnvAd\vec{l} = Id\vec{l}$, obtenemos entonces la siguiente relación
>$$  d\vec{B} = \frac{\mu_0}{4\pi} \frac{Id\vec{l} \times \hat{r}}{r^2} $$


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo-magnetico elemento-corriente.png" alt="Induccion por conexión a tierra">
    <figcaption>Campo magnético debido a un elemento de corriente </figcaption>
    </figure>
</div>
Una diferencia respecto al campo eléctrico es que este apunta en la dirección radial desde la carga puntual al punto donde observamos el campo (para una carga positiva), el campo magnético **es perpendicular** a $\hat{r}$ y $\vec{v}$, en caso de cargas puntuales y a $\hat{r}$ y $d\vec{l}$, en caso de un elemento de corriente. En un punto situado a lo largo de la línea, tal como el punto $P_2$ de la figura, **el campo magnético debido a dicho elemento es cero**.

> $d\vec{B} = 0$    si  $d\vec{l}$ y $\hat{r}$  son paralelos o antiparalelos


## Campo magnético $\vec{B}$ debido a una espira de corriente

### Campo magnético en el centro de una espira de corriente
Dado un elemento de corriente $Id\vec{l}$ de una espira de corriente de radio $R$ y el vector unitario $\hat{r}$ dirigido desde el elemento al centro de la espira. El campo magnético en el centro de la espira debido a este elemento está dirigido a lo largo del eje de la misma y su módulo viene dado por 
$$ dB = \frac{\mu_0}{4\pi} \frac{I \, dl\, sen\theta}{R^2} $$
donde $\theta$ es el ángulo que forman $dl$ y $\hat{r}$. Vemos que $sen(\theta)=1$ en cada elemento de corriente, además, como $R$ es constante, integrando la expresión anterior obtenemos
$$ 
B = \frac{\mu_0 \,I}{4\pi R^2} \oint dl = \frac{\mu_0 \,I}{2 R}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo-magnetico espira.png" alt="" width=350>
    <figcaption>Campo magnético producido por una espira de corriente </figcaption>
    </figure>
</div>

### Campo magnético en el eje de una espira de corriente
Consideremos el elemento de corriente situado en la parte superior de la espira. $Id\vec{l}$ es tangente a la espira y perpendicular el vector $\hat{r}$ dirigido desde el elemento de corriente al punto del campo $P$. El módulo de $d\vec{B}$ es
$$
|d\vec{B}| = \frac{\mu_0}{4\pi} \frac{I|d\vec{l} \times \hat{r}|}{r^2} = \frac{\mu_0}{4\pi} \frac{I\, dl}{(z^2 + R^2)}
$$
ya que $r^2 = z^2 + R^2$ y $d\vec{l}$ y $\hat{r}$ son perpendiculares, entonces $|d\vec{l} \times \hat{r}| = dl$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo-magnetico eje-espira.png" alt="">
    <figcaption>Campo magnético sobre el eje de una espira de corriente </figcaption>
    </figure>
</div>

Las componentes $dB_y$ suman cero, quedando solo las componentes $dB_z$ que son paralelas a este eje. 

$$
\begin{aligned}
dB_z &= dBsen(\theta) = \left(\frac{\mu_0}{4\pi} \frac{I\, dl}{(z^2 + R^2)}\right) \left(\frac{R}{\sqrt{z^2 + R^2}}\right) \\ \\
dB_z &= \frac{\mu_0}{4\pi} \frac{I R\, dl}{(z^2 + R^2)^{3/2}}
\end{aligned}
$$
Integrando al rededor de la espira
$$
B_z = \frac{\mu_0}{4\pi} \frac{I R}{(z^2 + R^2)^{3/2}} \oint dl = \frac{\mu_0 }{4 \pi} \frac{2 \pi I R^2}{(z^2 + R^2)^{3/2}}
$$


### Campo de un dipolo magnético en el eje de un dipolo
A grandes distancias de la espira, |z| es mucho mayor que $R$ de modo que 
$$
B_z = \frac{\mu_0}{4\pi} \frac{2I\pi R^2}{|z|^3}
$$

sea $\mu = I\pi R^2$ el módulo del momento magnético de la espira, se tiene que
$$
B_z = \frac{\mu_0}{4\pi} \frac{2 \mu}{|z|^3}
$$
> Podemos decir que el momento magnético de una espira es el producto punto entre la intensidad que pasa por esta y el área de la espira determinada por: (area) $\hat{n}$  es decir, un vector unitario normal al área y la magnitud del vector es la del área misma.


Una espira de corriente se comporta como un dipolo magnético, ya que experimenta un momento $\vec{\mu} \times \vec{B}$ cuando se sitúa en un campo magnético externo y también produce un campo dipolar magnético a gran distancia de la espira.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/lineas-campo espira.png" alt="">
    <figcaption>Líneas de campo magnético de una espira de corriente circular</figcaption>
    </figure>
</div>

## Campo magnético $\vec{B}$ debido a una corriente en un solenoide
Un solenoide es un alambre enrollado en forma de una hélice con espiras muy próximas entre sí. El solenoide se usa para producir un campo magnético intenso y uniforme en la región rodeada por sus espiras. Es análogo a un condensador que proporciona un campo uniforme entre sus placas.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/solenoide.png" alt="">
    <figcaption></figcaption>
    </figure>
</div>


El campo magnético de un solenoide es esencialmente el de una serie de $N$ espiras idénticas, situadas unas junto con otras.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo solenoide.png">
    <figcaption> </figcaption>
    </figure>
</div>


## Campo magnético en un solenoide largo y compacto
Consideremos un solenoide de longitud $L$ formado por $N$ vueltas de cable conductor que transporta una corriente de intensidad $I$. Sea un elemento de solenoide  de longitud $dz'$ a una distancia $z'$ del origen. Si $n = N/L$ es el número de vueltas por unidad de longitud, en este elemento existen $ndz'$ vueltas de alambre. Este elemento equivale a una simple espira que transporta una corriente $di = nIdz'$.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/solenoide largo compacto.png">
    <figcaption> </figcaption>
    </figure>
</div>
Sabemos que el campo magnético en un punto sobre el eje $z$ causado por una espira situada en el origen es
$$
B_z = \frac{\mu_0}{4 \pi} \frac{2 \pi I R^2}{(z^2 + R^2)^{3/2}} = \frac{1}{2} \mu_0 \frac{IR^2}{(z^2 + R^2)^{3/2}}
$$
Entonces , el campo dada una espira que transporta una corriente $nIdz'=di$ es
$$
dB_z = \frac{1}{2} \mu_0 \frac{R^2 di}{(z^2 + R^2)^{3/2}}
$$
donde $z$ es la distancia entre la espira y el punto donde se calcula el campo. Para una espira en $z=z'$, la corriente $di=nIdz'$, la distancia entre la espira y el punto del campo es $z-z'$, de esta forma tenemos que
$$
dB_z = \frac{1}{2} \mu_0 \frac{R^2 di}{((z-z')^2 + R^2)^{3/2}}
$$
Determinaremos el campo magnético debido al solenoide completo integrando esta expresión desde $z' = z_1$ a $z'=z_2$.
$$
B_z = \frac{1}{2} \mu_0 I R^2 \int_{z_1}^{z_2} \frac{dz'}{[(z-z')^2 + R^2]^{3/2}}
$$

Además haciendo $z-z'=Rtan(\theta)$
$$
\int_{z_1}^{z_2} \frac{dz'}{[(z-z')^2 + R^2]^{3/2}} = \frac{1}{R^2} \left( \frac{z-z_1}{\sqrt{(z-z_1)^2 + R^2}} - \frac{z-z_2}{\sqrt{(z-z_2)^2 + R^2}} \right)
$$

### Campo magnético en el eje de un solenoide
Por tanto el campo en un punto del eje del solenoide es
$$
B_z(z) = \frac{1}{2} \mu_0 \, n \, I \left( \frac{z-z_1}{\sqrt{(z-z_1)^2 + R^2}} - \frac{z-z_2}{\sqrt{(z-z_2)^2 + R^2}} \right)
$$

### Campo magnético en el interior de un solenoide largo
Un solenoide se considera largo si su longitud $L$ es mucho mayor que su radio $R$. Si analizamos la expresión entre paréntesis, esta se aproxima a 2, por tanto, el campo magnético dentro del solenoide y lejos de los extremos de este es
$$
B_z = \mu_0 n I
$$

## Campo magnético $\vec{B}$ debido a una corriente en un conductor rectilíneo
Calculemos el campo magnético en un punto $P$ debido a la corriente que circula por el segmento de alambre recto.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo magnetico conductor rectilineo.png">
    <figcaption> </figcaption>
    </figure>
</div>
Sea un elemento de corriente $Id\vec{l}$ situado a una distancia $x$ del origen. La dirección del campo magnético en $P$ debido al elemento de corriente esta dirigida hacia ti. Todos los elementos de corriente del conductor tienen la misma dirección, por tanto solo necesitamos calcular el módulo del campo.
$$
dB = \frac{\mu_0}{4\pi} \frac{Idx}{r^2} cos(\theta)
$$
Es preferible usar $\theta$ que $\phi$. Además, sabemos que $x=Rtan(\theta)$, $dx=Rsec^2 (\theta)  =\frac{r^2}{R}d\theta$. Sustituyendo en la expresión anterior, tenemos
$$
dB = \frac{\mu_0}{4\pi} \frac{I}{R} cos(\theta)d\theta
$$
Integrando desde $\theta_1$ hasta $\theta_2$ obtenemos
$$
B = \frac{\mu_0 I }{4\pi R}(sen\theta_2 - sen\theta_1)
$$

### Campo magnético debido a un conductor largo infinito
Si la longitud de un conductor tiene a infinito por ambos sentidos, $\theta_2 \to 90°$ y $\theta_1 \to -90°$, por tanto
$$
B = \frac{\mu_0 I }{2\pi R}
$$


## Fuerza magnética entre dos conductores paralelos

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo-magnetico eje-espira.png" alt="">
    <figcaption></figcaption>
    </figure>
</div>


# Ley de Gauss para el magnetismo
Si un extremo de una barra magnética esta incluido en una superficie gaussiana, el número de líneas del campo magnético que se alejan de la superficie es exactamente igual al número de las que entran en ella. Es decir, el flujo neto del campo a través de cualquier superficie cerrada es siempre cero.

> $$ \phi_{neto} = \oint_S \vec{B} \cdot \hat{n} \,d\,A = \oint_S B_n\,d\,A = 0 $$

Siendo $B_n$ la componente de $\vec{B}$ normal a la superficie $S$ en el elemento de area $dA$.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/lineas-campo-electrico y campo-magnetico.png" alt="">
    <figcaption>Comparación entre las líneas de campo de un dipolo eléctrico y un dipolo magnético</figcaption>
    </figure>
</div>


# Ley de Ampere

## Ley de Ampere
La ley de Ampere relaciona la integral de línea de la componente tangencial $B_t$ alrededor de una curva cerrada $C$ con la corriente $I_C$ que atraviesa la superficie limitada por dicha curva. Esta relación puede utilizarse para obtener una expresión del campo magnético en situaciones con un **alto grado de simetría**.
$$
\oint B_t \,d\vec{l} = \oint \vec{B} \cdot d\vec{l} = \mu_0\,I_C
$$
donde $I_C$ es la corriente neta que penetra en el área $S$ limitada por la curva $C$.

La ley de Ampere se cumple para cualquier curva siempre y cuando las corrientes sean estacionarias y continuas, es decir, que la corriente no varíe con el tiempo y que no haya acumulación espacial de carga.


## Ley de Ampere para un conductor largo rectilíneo
Dado un conductor infinitamente largo y rectilíneo portador de corriente. Sea una curva circular alrededor de un punto situado sobre el conductor que pasa por el centro de la curva. Según la ley de Biot-Savart, la dirección del campo magnético debido a cada elemento diferencial de corriente es tangente a esta circunferencia, por tanto, tienen la misma dirección que $d\vec{l}$, siendo su módulo constante en todo punto de la circunferencia.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/geoemtria conductor-largo-rectilineo.png" alt="">
    <figcaption>Ley de Ampere aplicado a un conductor largo y rectilíneo</figcaption>
    </figure>
</div>

La Ley de Ampere nos da lo siguiente
$$
B\oint_c dl = \mu_0\,I_c
$$
ya que $B$ tiene el mismo valor en todos los puntos de la circunferencia. La integral de $dl$ al rededor del circulo de radio $r$ es igual a $2\pi r$ y la intensidad $I_C$ es la que corresponde al alambre. Así, tenemos
$$
B (2\pi r) = \mu_0\,I_C
$$
$$
B = \frac{\mu_0\,I}{2\pi\,r}
$$

## Campo magnético $\vec{B}$ en el interior y exterior de un alambre



### Campo magnético $\vec{B}$ para u hilo recto largo (infinito)




## Campo magnético $\vec{B}$ en el interior de un toroide estrechamente enrollado
Tenemos  $N$ vueltas de conductor, cada una transportando una corriente $I$. Aplicaremos la ley de Ampere a una circunferencia de radio $r$, donde $a<r<b$, y centrada en el centro del toroide. La corriente que atraviesa la superficie de radio $r$ es $NI$. Además, por simetría, $\vec{B}$ es tangente a este círculo y constante en modulo en todos los puntos de la circunferencia. Tenemos por tanto
$$
B\oint_c dl = \mu_0\,I_c \rightarrow B(2\pi\,r) = \mu_0(NI)
$$
Despejando $B$
> $$ B = \frac{\mu_0\,NI}{2\pi r} \quad para\quad a<r<b $$


> Si $r<a$ no existe corriente que atraviese la superficie circular de radio $r$, por tanto el campo magnético es cero


>Si $r>a$ no existe corriente que atraviese la superficie circular de radio $r$, por tanto el campo magnético es cero
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/campo-magnetico toroide.png" alt=""width=400>
    <figcaption>Campo magnétio dentro de un toroide</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/radio-medio toroide.png" alt="" width=400>
    <figcaption>Radio medio de un toroide</figcaption>
    </figure>
</div>





# Resumen
![[Pasted image 20240614233607.png]]
![[Pasted image 20240614233631.png]]
![[Pasted image 20240614233700.png]]
