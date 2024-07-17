Las fem y las corrientes causadas por los flujos magnéticos variables se denominan **fem inducidas** y **corrientes inducidas**. En sí mismo, el proceso se denomina **inducción magnética**. Una fem producida cuando un conductor se mueve en una región en la que existe campo magnético se denomina **fem de movimiento**.

# Flujo magnético
El flujo magnético $\phi_m$ se define por la expresión
$$
\phi_m = \int_S \vec{B} \cdot \hat{n} \ dA = \int_S B_n \ dA  \tag{1}
$$
**Unidad**
Es el *tesla-metro cuadrado*  y se denomina **weber (Wb)**
$$
1 \ Wb = 1 \ T \cdot m^2
$$
Si la superficie es un plano de área $A$ y $\vec{B}$ es constante en módulo, dirección y sentido, sobre la superficie, el flujo que atraviesa la superficie es
$$
\phi_m = BA cos(\theta)
$$
donde $\theta$ es el ángulo entre la dirección de $\vec{B}$ y la normal a la superficie $\hat{n}$.

## Flujo magnético en una bobina
Si una bobina contiene $N$ vueltas, el flujo a través de la superficie es igual al producto de $N$ por el flujo que atraviesa una sola vuelta.
$$
\phi_m = NBAcos(\theta) \tag{2}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/flujo bobina.png" alt="Induccion por conexión a tierra" width=400>
    <figcaption>Flujo magnético en una bobina</figcaption>
    </figure>
</div>

# Fem inducida y Ley de Faraday

## Ley de Faraday
El flujo magnético a través de una superficie encerrada por un circuito puede alterarse de muchas maneras distintas. En cada uno de los casos, se induce una fem $\xi$ en el circuito cuyo valor es igual en módulo a la variación del flujo magnético por unidad de tiempo a través de (una superficie cerrada por) un circuito.
$$
\mathcal{E} = - \frac{d\phi_m}{dt} \tag{3}
$$
El signo negativo se debe al sentido de la fem inducida.

## Fem inducida en un circuito estacionario en un campo magnético variable
Los campos eléctricos que hemos estudiado previamente eran el resultado de cargas eléctricas estáticas. Estos campos son conservativos, lo cual significa que  su circulación alrededor de una curva cerrada $C$ es cero. (Se define la circulación del potencial vector $\vec{E}$ alrededor de la curva $C$ como $\oint \vec{E} \cdot d\vec{l}$). Sin embargo, el campo eléctrico resultante de un flujo magnético variable **no es conservativo**. La circulación alrededor de $C$ es una fem inducida igual a la variación con el tiempo del flujo magnético a través de cualquier superficie $S$ encerrada por $C$ cambiada de signo
$$
\mathcal{E} = \oint_C \vec{E}_{nc} \cdot d\vec{l} = - \frac{d}{dt} \int_S \vec{B} \cdot \hat{n} dA = -\frac{d\phi_m}{dt}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/fem inducida espira.png" alt="Induccion por conexión a tierra" width=400>
    <figcaption></figcaption>
    </figure>
</div>


# Ley de Lenz
El signo negativo de la ley de Faraday está relacionado con la dirección de la fem inducida. 
## Ley de Lenz

> [!info] Ley de Lenz
> La fem y la corriente inducidas poseen una dirección y sentido tal que tienden a oponerse a la variación que las produce

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/ley lenz.png">
    <figcaption></figcaption>
    </figure>
</div>


La siguiente figura muestra el momento magnético inducido en la espira de corriente cuando el imán se acerca hacia ella. La espira actúa como un imán con su polo norte a la izquierda y el sur a la derecha y dado que los polos iguales se repelen, el momento magnético inducido de la espira repele al imán, por lo que la espira reacciona oponiéndose al movimiento de acercamiento del imán a la espira, esto significa que el sentido de la corriente inducida en la espira tiene que ser tal como se muestra en la figura.



> [!info] Formulación alternativa de la ley de Lenz
> Cuando se produce una variación del flujo magnético que atraviesa una superficie, el campo magnético debido a la corriente inducida genera un flujo magnético sobre la misma superficie que se opone a dicha variación.


# Fem de movimiento

>[!info] Definición
>Fem de movimiento es toda fem inducida por el movimiento de un conductor en un campo magnético

## Carga total a través de una bobina que gira
Una pequeña bobina de $N$ vueltas está localizada en un plano perpendicular a un campo magnético uniforme $\vec{B}$,. La bobina está conectada a un integrador de corriente (C.I.), que es un dispositivo usado para medir la carga total que pasa por la bobina. Determinar la carga que atraviesa la bobina si esta gira $180^\circ$ alrededor del eje mostrado.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/carga bobina gira.png">
    <figcaption></figcaption>
    </figure>
</div>

Debemos recordar las ecuaciones
$$
\mathcal{E} = -\frac{d \phi}{dt} \ , \quad \xi = RI \ , \quad I = \frac{dq}{dt}
$$
Mediante un esfuerzo sobrehumano obtenemos
$$
Q = -\frac{1}{R} \int_{\phi_i}^{\phi_f} d\phi = -\frac{1}{R} (\phi_f - \phi_i)
$$

Al inicio, $\vec{B}$ y $\hat{n}$ comparten la misma dirección, y al final tienen direcciones opuestas, por tanto
$$
\Delta \phi = -2NBA
$$
y
$$
Q = \frac{2NBA}{R}
$$

## Modulo de la fem para una varilla que se mueve perpendicularmente a ella misma y a $\vec{B}$

La figura muestra una varilla conductora que se desliza a lo largo de dos conductores que están unidos a una resistencia. Existe un campo magnético $\vec{B}$ uniforme dirigido hacia la pantalla.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/modulo fem varilla movible.png">
    <figcaption></figcaption>
    </figure>
</div>


Considérese un flujo magnético a través de la superficie plana $S$ encerrada por el circuito. Sea $\mathbf{n}$ la normal a la superficie, un vector dirigido hacia dentro de la página. Como el área $S$ se incrementa cuando la varilla se mueve hacia la derecha, el flujo magnético a través de dicha superficie crece también y, por lo tanto, se induce una fem en el circuito. Si llamamos $\ell$ a la distancia que separa a los dos conductores que sirven de raíles y $x$ a la distancia desde el extremo izquierdo de los raíles a la varilla, el área $S$ encerrada por el circuito es $\ell x$, y el flujo magnético es

$$
\phi_m = \vec{B} \cdot \hat{n}A = B_n A = B \ell x
$$

Derivando con respecto del tiempo en ambos lados de la igualdad, se obtiene

$$
\frac{d\phi_m}{dt} = B\ell \frac{dx}{dt} = B \ell v
$$

en donde $v = dx/dt$ es la velocidad de la barra. Por lo tanto, la fem inducida en este circuito es

$$
\mathcal{E} = - \frac{d\phi_m}{dt} = -B \ell v
$$

donde el signo negativo significa que la fem se genera en la dirección tangencial negativa del circuito. Poniendo el dedo pulgar de la mano derecha en la dirección y el sentido del vector unitario $\hat{n}$ (hacia dentro de la pantalla) y los otros dedos curvándose en la dirección positiva, es decir, la horaria, vemos que la fem inducida lleva el sentido antihorario.

$$
|\mathcal{E}| = B \ell v
$$

Si el campo magnético no es perpendicular al plano del circuito, el campo $\vec{B}$ en la ecuación se debe sustituir por la componente normal de $\vec{B}$ en el plano del circuito.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/portador en una barra conductora.png">
    <figcaption></figcaption>
    </figure>
</div>


## Generadores y motores
Un generador simple de corriente alterna se construye con una bobina giratoria y un campo magnético uniforme tal como queda reflejado en la figura. Los extremos de la bobina se conectan a un anillo deslizante que gira con la bobina. El contacto eléctrico con la bobina se hace mediante un cepillo estacionario de grafito que debe estar en contacto con el anillo. 


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/generador.png">
    <figcaption></figcaption>
    </figure>
</div>



Cuando la perpendicular al plano de la bobina $\vec{n}$ forma un ángulo $\theta$ con el campo magnético uniforme $\vec{B}$, tal como se muestra en la figura, el flujo magnético a través de la bobina es


$$
\phi_m = NBA \cos \theta \tag{4}
$$


donde $N$ es el número de vueltas de la bobina y $A$ la superficie encerrada por ésta. Cuando la bobina gira mecánicamente, el flujo a través de ella varía y, como consecuencia, la fem se induce en la bobina de acuerdo con la ley de Faraday. Si el ángulo inicial entre $\vec{n}$ y $\vec{B}$ es cero, en un tiempo $t$, éste viene dado por

$$
\theta = \omega t
$$


donde $\omega$ es la velocidad angular de rotación. Sustituyendo esta expresión en la ecuación 4 obtenemos



$$
\phi_m = NBA \cos \omega t = NBA \cos 2 \pi f t
$$

La fem en la bobina es


$$
\mathcal{E} = - \frac{d \phi_m}{dt} = -NBA \frac{d}{dt} \cos \omega t = \omega NBA \sin \omega t \tag{5}
$$

^59d56c



Esto se puede escribir

$$
\mathcal{E} = \mathcal{E}_{\text{máx}} \sin \omega t
$$
donde
$$
\mathcal{E}_{\text{máx}} = \omega NBA
$$

es el máximo valor de la fem. **Si giramos la bobina con una velocidad angular constante en el seno de un campo magnético se produce una fem sinusoidal**. De esta forma, la energía mecánica de rotación se convierte en energía eléctrica.
# Inductancia

## Autoinducción
Consideremos una bobina por la que circula una corriente $I$. La corriente produce un campo magnético $\vec{B}$ que varía de un punto a otro, pero en todos los puntos $\vec{B}$ es proporcional a $I$. El flujo magnético a través de la bobina, por lo tanto, es también proporcional a $I$:

$$
\phi_m = LI \tag{6}
$$

donde **$L$ es una constante llamada autoinducción de la bobina**. La autoinducción depende de la forma geométrica de la bobina. La unidad del SI de inductancia es el henry (H) y según la ecuación 6 es igual a la unidad de flujo, el weber, dividido por la unidad de intensidad de corriente, el ampere:

$$
1 \, \text{H} = 1 \, \text{Wb/A} = 1 \, \text{T} \cdot \text{m}^2 / \text{A}
$$

En principio, la autoinducción de cualquier bobina o circuito puede calcularse suponiendo la existencia de una corriente $I$ determinada $\vec{B}$ en cada punto de una superficie encerrada por la bobina, calculando el flujo $\phi_m$ y usando la ecuación $L = \phi_m / I$. 
En la práctica, el cálculo es muy difícil. Sin embargo, **la autoinducción de un solenoide enrollado apretadamente puede calcularse directamente**. 

### Autoinducción de un solenoide
El campo magnético en un solenoide de estas características, de longitud $l$ y área de la sección transversal $A$, por lo tanto, el flujo sería:

$$
\phi_m = NBA = \mu_0 N (\mu_0 n I) A = \frac{\mu_0 N^2 I A}{l} = \mu_0 n^2 I A l \tag{7}
$$

donde $n = N / l$ es el número de vueltas por unidad de longitud. Como es lógico, el flujo es proporcional a la intensidad de corriente $I$. La constante de proporcionalidad es la autoinducción

$$
L = \frac{\phi_m}{I} = \mu_0 n^2 A l \tag{8}
$$

La autoinducción es proporcional al cuadrado del número de vueltas por unidad de longitud $n$ y al volumen $Al$. Así pues, lo mismo que la capacidad, **la autoinducción depende sólo de factores geométricos**. 


### Fuerza electromotriz autoinducida
Cuando la intensidad de corriente de un circuito varía, el flujo magnético debido a la corriente también se modifica y, por lo tanto, en el circuito se induce una fem. Como la autoinducción del circuito es constante, la variación del flujo está relacionada con la variación de intensidad por

$$
\frac{d\phi_m}{dt} = \frac{d (LI)}{dt} = L \frac{dI}{dt}
$$

De acuerdo con la ley de Faraday, resulta

$$
\mathcal{E} = - \frac{d\phi_m}{dt} = - L \frac{dI}{dt} \tag{9}
$$


Así pues, la fem autoinducida es proporcional a la variación con el tiempo de la intensidad de corriente. **Una bobina o solenoide con suficientes vueltas para tener alta autoinducción se denomina inductor**. En los circuitos se representa con el símbolo $\sim$. Generalmente, podemos despreciar la autoinducción del resto del circuito comparado con la de un inductor. 

### Diferencia de potencial entre los extremos de un inductor
La diferencia de potencial entre los extremos de un inductor viene dada por
$$
\Delta V = \mathcal{E} - I r = - L \frac{dI}{dt} - I r \tag{10}
$$

donde $r$ es la resistencia interna del inductor. Para un inductor ideal, $r = 0$.

## Inductancia mutua
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/inductancia mutua.png">
    <figcaption></figcaption>
    </figure>
</div>

Cuando dos o más circuitos están próximos uno al otro, como indica la figura anterior, el flujo magnético que atraviesa uno de ellos depende no sólo de la corriente en este circuito, sino también de la corriente que circula por los circuitos próximos. Sea $I_1$ la corriente en el circuito 1 de la izquierda de la figura  e $I_2$ la del circuito 2 de la derecha. El campo magnético $\vec{B}$ en la superficie $S_2$ es la superposición de $\vec{B}_1$, debido a $I_1$ y $\vec{B}_2$ debido a $I_2$, siendo $B_1$ proporcional a $I_1$ (y $B_2$ proporcional a $I_2$). Por lo tanto, podemos expresar el flujo de $B_1$ que atraviesa el circuito 2, $\phi_{m21}$ como

$$
\phi_{m12} = M_{12} I_1 \tag{11}
$$

donde $M_{12}$ es la inductancia mutua de los dos circuitos. La inductancia mutua depende de la disposición geométrica entre ambos. En particular, podemos ver que si los circuitos están bastante separados, el flujo de $B_1$ a través del circuito 2 será pequeño y la inductancia mutua también lo será. (El flujo neto $\phi_{m2}$ de $\vec{B}$ = $\vec{B}_1 + \vec{B}_2$ que atraviesa el circuito 2 es $\phi_{m2} = \phi_{m12} + \phi_{m2.2}$) Puede escribirse una ecuación semejante a la 28.16a para el flujo de $\vec{B}_2$ que atraviesa el circuito 1:

$$
\phi_{m21} = M_{21} I_2 \tag{28.16b}
$$

Podemos calcular la inductancia mutua de dos solenoides concéntricos de espiras apretadas como los que se muestran en la figura 28.28. Sea $\ell$ la longitud común de ambos solenoides y supongamos que el solenoide interior tiene $N_1$ vueltas y radio $r_1$ y que el solenoide exterior tiene $N_2$ vueltas y radio $r_2$. Calcularemos primero la inductancia mutua $M_{21}$ suponiendo que el solenoide interior transporta una corriente $I_1$ y determinando el flujo magnético $\phi_{m2}$ debido a esta corriente a través del solenoide exterior.

El campo magnético $\vec{B}_1$ debido a la corriente del solenoide interno es constante en su espacio interior y su valor es

$$
B_1 = \mu_0 (N_1 / \ell) I_1 = \mu_0 n_1 I_1 \quad r < r_1 \tag{28.17}
$$

Fuera del solenoide interno, el campo magnético $B_1$ es despreciable. El flujo de $\vec{B}_1$ que atraviesa el solenoide externo debido a este campo magnético es, por lo tanto,

$$
\phi_{m2} = N_2 B_1 (\pi r_1^2) = n_2 \ell B_1 (\pi r_1^2) = \mu_0 n_2 n_1 \ell (\pi r_1^2) I_1
$$

Obsérvese que el área utilizada para calcular el flujo que atraviesa el solenoide exterior no es el área de dicho solenoide, $\pi r_2^2$, sino el área del solenoide interior $\pi r_1^2$, ya que el campo magnético debido al solenoide interior es cero fuera del mismo. La inductancia mutua es, por lo tanto,

$$
M_{12} = \frac{\phi_{m12}}{I_1} = \mu_0 n_2 n_1 \ell (\pi r_1^2) \tag{28.18}
$$


# Energía magnética
Un inductor almacena energía magnética, del mismo modo que un condensador almacena energía eléctrica. Consideremos el circuito formado por una inductancia $L$ y una resistencia $R$ en serie con una batería de fem $\mathcal{E}_0$ y un interruptor $S$, como se muestra en la figurax


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/circuito RL.png">
    <figcaption></figcaption>
    </figure>
</div>


Se supone que $R$ y $L$ son la resistencia e inductancia del circuito completo. El interruptor está inicialmente abierto, de modo que no pasa corriente por el circuito. Poco después se cierra el interruptor y aparece una corriente $I$ en el circuito, una caída de potencial $-IR$ a través de la resistencia y una diferencia de potencial $-L \, dI / dt$ en el inductor. (En un inductor de resistencia despreciable, la diferencia de potencial entre sus extremos es igual a la fuerza contra-electromotriz, la cual se expresa en la ecuación 28.14.) Aplicando la ley de las mallas de Kirchhoff en este circuito, resulta

$$
\mathcal{E}_0 - IR - L \frac{dI}{dt} = 0 \tag{15}
$$

Multiplicando ambos miembros de la ecuación anterior por la intensidad de corriente $I$, resulta

$$
\mathcal{E}_0 I = I^2 R + L I \frac{dI}{dt} \tag{16}
$$

El término $\mathcal{E}_0 I$ es la potencia suministrada por la batería. El término $I^2 R$ es la energía potencial por unidad de tiempo que incide en la resistencia. (También es la potencia disipada en forma de calor en la resistencia del circuito.) El término $L I \, dI / dt$ representa la energía que por unidad de tiempo incide en el inductor. 


### Energía almacenada en un inductor
Si $U_m$ es la energía en el inductor, se verifica

$$
\frac{dU_m}{dt} = L I \frac{dI}{dt}
$$

o también,

$$
dU_m = L I \, dI
$$

Integrando esta ecuación, resulta:

$$
U_m = \frac{1}{2} LI^2 + C
$$

donde $C$ es una constante de integración. Para obtener $C$, igualamos $U_m$ a cero cuando $I$ es igual a cero. La energía almacenada en un inductor que transporta una corriente $I$ viene dada por

> [!info] Energía almacenada en un inductor
>$$ U_m = \frac{1}{2} LI^2 \tag{17} $$


### Densidad de energía
En el proceso de producir una corriente en un inductor, se crea un campo magnético en el espacio interior de su bobina. Es decir, **podemos imaginar que la energía almacenada en un inductor es energía almacenada en el campo magnético creado**. En el caso especial de un solenoide largo, el campo magnético está relacionado con la corriente $I$ y el número de vueltas por unidad de longitud $n$ por

$$
B = \mu_0 n I
$$

y la autoinducción viene expresada por la ecuación 8: $L = \mu_0 n^2 A \ell$ en donde $A$ es el área transversal y $\ell$ la longitud. Sustituyendo $I$ por $B / (\mu_0 n)$ y $L$ por $\mu_0 n^2 A \ell$ en la ecuación 17, resulta

$$
U_m = \frac{1}{2} LI^2 = \frac{1}{2} \mu_0 n^2 A \ell \left( \frac{B}{\mu_0 n} \right)^2 = \frac{B^2}{2 \mu_0} A \ell
$$

La magnitud $A \ell$ es el volumen del espacio contenido dentro del solenoide, donde se crea el campo magnético. La energía por unidad de volumen es la **densidad de energía magnética** $u_m$

$$
u_m = \frac{1}{2} \frac{B^2}{\mu_0} \tag{18}
$$

Aunque esta ecuación se ha obtenido para el caso especial del campo magnético en un solenoide largo, el resultado es general. Es decir, siempre que exista un campo magnético en el espacio, la energía magnética por unidad de volumen viene dada por la ecuación 28.22. Obsérvese la semejanza con la densidad de energía eléctrica en un campo eléctrico de la [[Condensadores o capacitores#Energía del campo electrostático#Densidad de energía de un campo electrostático|ecuación]].

# Circuitos RL

Un circuito que contiene una resistencia y un inductor tal como el indicado en la [[circuito RL.png|figura]] anterior  se denomina **circuito RL**. Como a temperatura ambiente todos los circuitos contienen resistencia y autoinducción, el análisis de un circuito RL puede aplicarse en cierta extensión a todo circuito.

Para el circuito de la figura  [[circuito RL.png|figura]] , la aplicación de la regla de las mallas de Kirchhoff nos dio:

$$
\mathcal{E}_0 - IR - L \frac{dI}{dt} = 0 \tag{19}
$$

Podemos entender muchas de las características de la corriente en este circuito a partir de la ecuación anterior sin necesidad de resolverla. Inicialmente (justo después de cerrar el interruptor) la corriente es nula, de modo que $IR$ es cero y $L \, dI / dt$ es igual a la fem de la batería, $\mathcal{E}_0$. Haciendo $I = 0$ en la ecuación 19, resulta

$$
\frac{dI}{dt} \bigg|_{t=0} = \frac{\mathcal{E}_0}{L} \tag{20}
$$

Cuando la corriente crece, $IR$ crece también y $dI / dt$ disminuye. Obsérvese que la corriente no puede saltar súbitamente de cero a un valor finito como lo haría si no tuviera inductancia. Cuando la inductancia $L$ no es despreciable, $dI / dt$ es finita y, por lo tanto, la corriente debe ser continua en el tiempo. En un tiempo breve, la corriente alcanza un valor positivo $I$, y su variación con el tiempo es

$$
\frac{dI}{dt} = \frac{\mathcal{E}_0 - IR}{L}
$$

En este momento la corriente es todavía creciente, pero su ritmo de crecimiento es menor que en el instante $t = 0$. El valor final de la corriente puede obtenerse haciendo $dI / dt$ igual a cero. El valor final de la corriente es, por lo tanto,

$$
I_f = \frac{\mathcal{E}_0}{R} \tag{20}
$$

La siguiente figura muestra la variación de la corriente en este circuito en función del tiempo. Esta figura es semejante a la que representa la variación de la carga en un condensador cuando éste se carga en un circuito RC (figura 25.45).

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/grafica corriente tiempo.png">
    <figcaption></figcaption>
    </figure>
</div>

La ecuación 19 tiene la misma forma que la ecuación 25.38 correspondiente a la carga de un condensador y puede resolverse de igual modo, es decir, separando variables e integrando. El resultado es

$$
I = \frac{\mathcal{E}_0}{R} (1 - e^{-(R/L)t}) = I_f (1 - e^{-t/\tau}) \tag{21}
$$

donde $I_f = \mathcal{E}_0 / R$ es la corriente cuando $t \to \infty$,

$$
\tau = \frac{L}{R} \tag{22}
$$

es la **constante de tiempo** del circuito. Cuanto mayor es la autoinducción $L$ o menor la resistencia $R$, más tiempo exige el establecimiento de una fracción determinada de la corriente final $I_f$.


En la siguiente figura, el circuito posee un interruptor adicional que nos permite eliminar la batería del circuito sin interrumpir la corriente que circula por el inductor, y una resistencia adicional $R_1$ para proteger a la batería, de modo que no resulte cortocircuitada cuando el interruptor hace contacto. 

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/circuito RL 1.png">
    <figcaption></figcaption>
    </figure>
</div>



Si el interruptor está en la posición $e$, la batería, el inductor y las dos resistencias se encuentran conectadas en serie, y la corriente crece en el circuito del modo que acabamos de analizar, excepto en que ahora la resistencia total es $R_1 + R$ y la corriente final $\mathcal{E}_0/(R + R_1)$. Supongamos que el polo del interruptor ha permanecido en la posición $e$ durante un tiempo largo, de modo que la corriente es aproximadamente estacionaria en su valor final, que llamaremos $I_0$. En el tiempo $t = 0$ movemos rápidamente el polo a la posición $f$ (para eliminar la batería de cualquier consideración). Tenemos ahora un circuito que tiene sólo una resistencia y una bobina (malla $abcdefa$) sobre las cuales circula una corriente inicial $I_0$. Aplicando la regla de las mallas de Kirchhoff a este circuito, resulta

$$
-IR - L \frac{dI}{dt} = 0
$$

Reajustando esta ecuación para separar las variables $I$ y $t$, se obtiene

$$
\frac{dI}{I} = -\frac{R}{L} dt \tag{23}
$$

La ecuación 28.27 es de la misma forma que la ecuación 25.34 correspondiente a la descarga de un condensador. Integrando y despejando $I$, se llega a

$$
I = I_0 e^{-t/\tau} \tag{24}
$$

en donde $\tau = L / R$ es la constante de tiempo. La figura 28.33 muestra la corriente en función de tiempo.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/grafica intensidad circuito RL 1.png">
    <figcaption></figcaption>
    </figure>
</div>








