# Fuerza ejercida por un campo magnético
Cuando una carga q posee la velocidad $\vec{v}$ en un campo magnético, aparece una fuerza que es proporcional a $q$ y $v$ y al seno del ángulo que forman $\vec{v}$ y $\vec{B}$.  La fuerza es perpendicular al plano que forman estos vectores.
## Fuerza magnético sobre una carga móvil
> $$ \vec{F} = q\vec{v} \times \vec{B} $$

La existencia de un campo magnético $\vec{B}$ en un punto del espacio puede demostrarse con una brújula. **Si existe un campo magnético, la aguja se alineará en la dirección de este campo**.

### Fuerza de Lorentz
Cuando hay también un **campo eléctrico** $\vec{E}$, la fuerza total sobre una carga de prueba es la **Fuerza de Lorentz**
$$ \vec{F} = q(\vec{E} + \vec{v}\vec{B}) $$

### Unidad del SI
La unidad del campo magnético es el **tesla (T)**. Una carga de un coulomb que se mueve a un metro por segundo perpendicular a un campo magnético de un tesla, experimenta una fuerza de un newton:
$$ 1 \, T = 1 \, \frac{F}{C \cdot m/s} = 1 \, N / (A \cdot m) $$
Esta unidad es bastante grande. El campo magnético terrestre es algo menos que $10^{-4} \, T$ en la superficie de la Tierra. Una unidad habitualmente, deducida del sistema $cgs$, es el **gauss (G)**, que está relacionada con el tesla por
$$ 1 \, G = 10^{-4} \, T $$

## Fuerza magnética sobre un segmento de alambre portador de corriente

Cuando por un cable situado en el interior de un campo magnético circula una corriente, existe una fuerza que se ejerce sobre el conductor que es simplemente la suma de las fuerzas magnéticas sobre las partículas cargadas cuyo movimiento produce la corriente.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/segmento-alambre-corriente.png" alt="Induccion por conexión a tierra">
    <figcaption>Segmento de alambre de longitud L que transporta una carga de intensidad </figcaption>
    </figure>
</div>

La fuerza magnética sobre un conjunto de cargas
$$  
\vec{F} = \sum_i \, q_i \, \vec{v}_i \times \vec{B}
$$
La velocidad de desplazamiento de los portadores de carga  $\vec{v}$  es la misma que su velocidad media. El número de cargas en el interior del segmento de alambre es el número $n$ que hay por unidad de volumen multiplicado por el volumen $A \,dl$. Así pues, la fuerza total sobre el segmento del cable es

$$ d\vec{F} = (q\vec{v_d} \times \vec{B})n \, A \, dl $$
donde $n$ es la densidad de partículas por unidad de volumen y $v_d$ la velocidad de desplazamiento media.
La densidad de carga $\rho=qn$, el elemento de volumen es $d\,V=A\,d\,l$, entonces
$$ d\vec{F} = (\rho\, \vec{v_d} \times \vec{B}) \, dV  $$
Como la  [[Corriente eléctrica y circuitos de corriente continua#Densidad de corriente|densidad de corriente]]  es $\vec{J} = \rho \, \vec{v_d}$, entonces $d\vec{F} = (\vec{J} \times \vec{B}) \, dV$. Tenemos entonces

$$
\vec{F} = \int (\vec{J} \times \vec{B}) \, dV
$$
.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/fuerza-magnetica alambre-corriente.png" alt="Induccion por conexión a tierra">
    <figcaption>Fuerza magnética sobre un segmento de alambre portador de corriente en un campo magnético</figcaption>
    </figure>
</div>

## Fuerza magnética sobre un elemento de corriente
Se generaliza el caso de un **conductor de forma arbitraria** en el interior de un **campo magnético cualquiera**. De la ecuación anterior, teníamos
$$ d\vec{F} = (q\vec{v_d} \times \vec{B})n \, A \, dl $$
donde $I=nqv_dA$. Para un segmento de hilo $d \vec{l}$, la fuerza que actual sobre dicho segmento $\vec{F}$, viene dada por
$$ 
d\vec{F} = I \, d\vec{l} \times \vec{B} 
$$

## Líneas de campo magnético
La dirección y sentido del campo vienen indicados por la dirección y el sentido de las líneas de campo y el módulo del campo por su densidad.
1. Las líneas de campo magnético son perpendiculares a la fuerza magnética sobre una carga móvil.
2. Las líneas de campo magnético son cerradas.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Lineas-campo-magnetico.png" alt="Induccion por conexión a tierra">
    <figcaption>Líneas de campo magnético dentro y fuera de una barra magnética </figcaption>
    </figure>
</div>

# Movimiento de una carga puntual en un campo magnético

La fuerza magnética modifica la dirección de la velocidad, pero no su módulo. 

> - Los campos magnéticos no realizan trabajo sobre las partículas y no modifican su energía cinética
>- La fuerza es central si $B$ es **constante**, el módulo de la fuerza también y el movimiento  de la carga es un **MCU**.


## Periodo y frecuencia de un ciclotrón
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/particula-plano-perpendicular-campo.png" alt="Induccion por conexión a tierra" width=300>
    <figcaption>Partícula cargada que se mueve en un plano perpendicular a un campo uniforme</figcaption>
    </figure>
</div>

En la figura, la fuerza magnética proporciona la fuerza centrípeta necesaria para que la partícula adquiera la aceleración centrípeta $v^2/r$ del movimiento circular. Como $\vec{v}$ y $\vec{B}$ son perpendiculares, el módulo de la fuerza es $qvB$ y por la segunda ley de Newton
$$ 
\begin{aligned}
F &= ma \\ \\
qvB &= m \frac{v^2}{r} \\ \\
r &= \frac{mv}{qB} \quad \text{Radio de Larmor}
\end{aligned}
$$

donde $m$ es la masa de la partícula. 

### Periodo del ciclotrón
El periodo del movimiento circular es $T = 2 \pi r/ v$, usando la expresión para $r$, podemos obtener el periodo del movimiento circular o **periodo del ciclotrón**
$$ T = \frac{2\pi (mv/qB)}{v} = \frac{2\pi m}{qB} $$

### Frecuencia del ciclotrón
La frecuencia del ciclotrón es el recíproco del periodo. 
$$ f = \frac{1}{T} = \frac{qB}{2\pi \,m} $$
  
 Teniendo en cuenta que $\omega = 2\pi f$, donde $\omega$ es la velocidad angular,
 $$ \omega = 2\pi f = \frac{q}{m}B $$
 > El periodo y la frecuencia ($\omega$) dependen de la relación carga/masa $q / m$ pero son independientes del radio $r$ y de la velocidad $v$.



Si una partícula cargada entra en una region del espacio, donde existe un campo magnético $\vec{B}$ uniforme con una velocidad $\vec{v}$ que no es perpendicular a $\vec{B}$, entonces, $\vec{B}$ se puede descomponer en una componente paralela a $\vec{v}$ $B_{//}$ y una componente perpendicular $\vec{v}$ $B_{\perp}$ . En este caso, $\vec{v} \times B_{//}$ no produce una fuerza, pero $\vec{v} \times B_{\perp}$ si genera una fuerza, entonces el movimiento de la partícula cargada queda afectada por la fuerza generada por 
$$ q \, \vec{v} \times B_{\perp} $$
la cual hace que la partícula tenga un movimiento **MCU**, sin embargo, también sigue manteniendo su velocidad $\vec{v}$ por tanto, **la partícula tiene un movimiento helicoidal**.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/movimiento helice particula.png" alt="Induccion por conexión a tierra">
    <figcaption>Movimiento helicoidal de una partícula</figcaption>
    </figure>
</div>

## Selector de velocidades
Puesto que la fuerza eléctrica tiene la dirección y el sentido del campo magnético (para cargas positivas) y la fuerza magnética es perpendicular al campo magnético, los campos eléctrico y magnético deben ser perpendiculares entre sí para que se contrarresten estas fuerzas. Una región de estas características se dice que tiene los **campos cruzados**.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/selector velocidades.png" alt="" width=400>
    <figcaption>Selector de velocidades</figcaption>
    </figure>
</div>

Según la figura, consideremos una partícula de carga $q$ entrando a la región entre dos placas de un condensador desde la izquierda. La fuerza neta sobre la partícula es

$$
\vec{F} = q\vec{E} + q\vec{v} \times \vec{B}
$$

Si la carga es negativa, las direcciones de las fuerzas estarán invertidas. Las dos fuerzas se equilibrarán si $qE = qvB$, es decir,
$$
v = \frac{E}{B}
$$
Cualquier partícula con esta velocidad, independientemente de su masa o carga, atravesará el espacio sin desviarse. Un dispositivo de campos de esta forma se denomina **selector de velocidades**. Solo pasarán y serán seleccionadas aquellas partículas cuya velocidad venga dada por la ecuación $v=E/B$.

## Espectrómetro de masas (Aston - 1919)
Fue diseñado para medir las masas de los isótopos. Según el dibujo esquemático, los iones positivos se consiguen bombardeando átomos neutros con rayos X o con un haz de electrones. (Los electrones se extraen de los átomos mediante rayos X o mediante electrones de bombardeo). Estos iones son acelerados por un campo eléctrico y entran en un campo magnético uniforme. Si los iones positivos parten del reposo y se mueven a través de una diferencia de potencial $\Delta V$, su energía cinética cuando entran en el campo magnético es igual a la pérdida de energía potencial, $q|\Delta V|$:
$$
\frac{1}{2}mv^2 = q|\Delta V|
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/espectromatro masas.png" alt="" width=350>
    <figcaption>Dibujo esquemático de un espectrómetro de masas</figcaption>
    </figure>
</div>

Los iones se mueven en una semicircunferencia de radio r dada la [[#Periodo y frecuencia de un ciclotrón|ecuación]] $r=mv/qB$, e inciden sobre una película fotográfica en el punto $P_2$, a una distancia $2r$ del punto $P_1$ por el que entraron en el campo magnético.

De $r=mv/qB$ y $\frac{1}{2}mv^2 = q|\Delta V|$ se obtiene
$$
\frac{1}{2}m \left(\frac{r^2q^2B^2}{m^2}\right) = q|\Delta V|
$$
Simplificando y despejando $m/q$, resulta
> $$ \frac{m}{q} = \frac{B^2r^2}{2 \, |\Delta V|} $$


# Momentos de fuerza sobre espiras de corriente e imanes

Una espira de corriente **no experimenta ninguna fuerza neta** cuando se encuentra en un campo magnético uniforme, pero sobre ella se ejerce un par que tiende a girarla. La orientación de la espira se describe mediante un vector unitario $\hat{n}$ que es perpendicular al plano de la espira. Si los dedos de la mano derecha se curvan en el mismo sentido que la corriente de la espira, su dedo pulgar apunta en la dirección de $\hat{n}$.
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/momento-dipolar espira-rectangular.png" alt=""  width=600>
    <figcaption>Espira de corriente rectangular</figcaption>
    </figure>
</div>

El vector $\hat{n}$ forma un ángulo $\theta$ con el campo magnético $\vec{B}$. La fuerza neta es cero. Las fuerzas $\vec{F_1}$ y $\vec{F_2}$ tienen el módulo
$$
F_1 = F_2 = IaB
$$
La magnitud del momento es
$$
\tau = F_2 \, b\,sen\theta = IaB\,bsen\theta = IAB\,sen\theta
$$
donde $A=ab$ es el área de la espira. Si esta posee $N$ vueltas, el momento tiene el módulo
$$
\tau = NIAB\,sen\theta
$$
**Este momento tiende a girar la espira de modo que el vector $\hat{n}$ tenga la misma dirección que** $\vec{B}$

## Momento dipolar magnético de una espira de corriente
El momento puede escribirse de forma adecuada en función del **momento dipolar magnético** $\mu$ (simplemente **momento magnético**) de la espira de corriente, definido por
$$
\vec{\mu} = NIA\hat{n} \quad \quad (A \cdot m^2) 
$$
donde $I$ es la corriente, $A$ es el área de la espira y $\hat{n}$ tiene la misma dirección que el dedo pulgar cuando orientamos los dedos de la mano derecha con la orientación de la corriente.

## Momento sobre una espira de corriente
La unidad del momento magnético es ($A\cdot m^2$). En función del momento dipolar magnético, el momento sobre la espira de corriente viene dado por
$$
\vec{\tau} = \vec{\mu} \times \vec{B}
$$
La ecuación anterior es válida en general para una espira de cualquier forma.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/momento-magnético espira-plana.png" alt="Induccion por conexión a tierra">
    <figcaption>Espira plana de corriente de forma arbitraria</figcaption>
    </figure>
</div>
**Una espira de corriente situada en un campo magnético actúa del mismo modo que un dipolo eléctrico situado en un campo eléctrico**.


## Energía potencial de un dipolo magnético en un campo magnético
Cuando un momento actúa sobre un objeto y este gira un determinado ángulo, se realiza trabajo. Cuando un dipolo gira un ángulo $d\theta$, el trabajo realizado es
$$
dW = -\tau d\theta = -\mu B\,sen\theta
$$
donde $\theta$ es es ángulo entre $\vec{u}$ y $\vec{B}$. El signo menos aparece porque el momento tiende a disminuir el ángulo $\theta$. El trabajo se debe a la disminución de energía potencial, entonces
$$
dU = -dW = -\tau d\theta = +\mu B\,sen\theta
$$
Integrando obtenemos
$$
U =  -\mu B\,cos\theta + U_0
$$
Si elegimos la energía potencial de modo que sea cero en $\theta=90$, resulta que $U_0=0$ y la energía potencial de dipolo es
$$
U =  -\mu B\,cos\theta = -\vec{\mu} \cdot \vec{B}
$$


## Momento magnético $\mu$ de un disco en movimiento rotatorio


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/disco-rotatorio.png" alt="" width=350>
    <figcaption>Momento en un disco rotatorio</figcaption>
    </figure>
</div>

# Efecto Hall
Cuando las cargas se mueven en un campo magnético experimentan una fuerza perpendicular a su movimiento. Por lo tanto, si estas cargas se desplazan en un **alambre conductor**, serán impulsadas hacia un lado del alambre. Debido a esto se produce una separación de carga en el alambre denominada **Efecto Hall**. 

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/efecto-Hall.png" alt="Induccion por conexión a tierra">
    <figcaption>Efecto Hall</figcaption>
    </figure>
</div>

Supongamos que la corriente está formada por partículas positivamente cargadas que se mueven hacia la derecha como la figura de la izquierda. La fuerza magnética esta dirigida hacia arriba. Las partículas positivas, por lo tanto, se mueven hacia la parte superior de la cinta, dejando el fondo de la misma con un exceso de carga negativa. Esta separación de carga **produce un campo electrostático** en la cinta que se opone a la fuerza magnética que actúa sobre los portadores de carga. Cuando las fuerzas electrostática y magnética se equilibran, los portadores de carga dejan de moverse hacia arriba. En este caso, la parte superior de la cinta esta a mayor potencial que la parte inferior. [[Potencial eléctrico#Potencial y líneas de campo eléctrico|Anotación]]. 

Por otro lado, si la corriente consta de partículas cargadas negativamente, como la figura de la derecha, los portadores de cargas se mueven hacia la izquierda. La fuerza magnética se dirige de nuevo hacia arriba. De nuevo, los portadores son forzados a la parte superior de la cinta, pero como ahora estos son negativos, la carga negativa se acumula en la parte superior de la cinta y la carga positiva en la parte inferior.

- Una medida del signo de la diferencia de potencial entra la superior e inferior de la cinta nos dirá el signo de los portadores de carga. 
- Una medida del signo de la diferencia de potencial nos dice cuales son los portadores de carga dominantes en un semiconductor particular.

**Este fue el tipo de experimento que condujo al descubrimiento de que los portadores de carga en los conductores metálicos son negativos**.

La diferencia de potencial entre la parte superior e inferior de la cinta se llama **voltaje de Hall** y puede calcularse en función de la velocidad de desplazamiento. El módulo de la fuerza magnética es $qv_dB$. Esta fuerza es equilibrada por la fuerza electrostática de módulo $qE_H$, en donde $E_H$ es el campo debido a la separación de cargas. Como ambas fuerzas están en equilibrio, tenemos que $E_H = v_d\,B$ [[#Selector de velocidades|Anotación]]. Si la anchura de la cinta es $w$, la diferencia de potencial es $E_Hw$. Por lo tanto, el voltaje Hall es
$$
V_H = E_H\,w = v_dBw
$$
A partir de medidas del valor del voltaje Hall para una cinta de un tamaño determinado, podemos determinar el número de portadores de carga por unidad de volumen de la cinta. Según la [[Corriente eléctrica y circuitos de corriente continua#Relación entre la intensidad y la velocidad de desplazamiento|ecuación]], la intensidad de corriente es
$$
|I| = |q|nv_dA
$$
donde $A$ es la sección transversal de la cinta. Sea $t$ el espesor de la cinta, $A=wt$. Como los portadores de carga son electrones, el valor de $|q|$ es la carga de un electrón $e$. La densidad numérica de los portadores de carga $n$ viene dada por
$$
n = \frac{|I|}{A|q|v_d} = \frac{|I|}{w\,t\,ev_d}
$$
y como $v_dw=V_H/B$, tenemos 
$$
n = \frac{|I|B}{t\,eV_H}
$$
El voltaje de Hall proporciona un método conveniente para medir campos magnéticos. Dada la expresión
$$
V_H = \frac{|I|}{nte}B
$$
Una cinta puede calibrarse midiendo el voltaje Hall para una determinada intensidad de corriente en un campo magnético conocido. La intensidad de un campo magnético $B$ desconocido puede entonces medirse situando la cinta en este campo, haciendo circular una corriente conocida por la cinta y midiendo $V_H$.

# Resumen

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/resumen1-campo-magnetico.png" alt="Induccion por conexión a tierra">
    <figcaption>Resumen 1</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/resumen2-campo-magnetico.png" alt="Induccion por conexión a tierra">
    <figcaption>Resumen 2</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/resumen3-campo-magnetico.png" alt="Induccion por conexión a tierra">
    <figcaption>Resumen 3</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/resumen4-campo-magnetico.png" alt="Induccion por conexión a tierra">
    <figcaption>Resumen 4</figcaption>
    </figure>
</div>



