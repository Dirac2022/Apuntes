En Norteamérica, la potencia eléctrica se suministra mediante una corriente sinusoidal de 60 Hz, mientras que en prácticamente todo el resto del mundo la frecuencia es de 50 Hz. 
La corriente alterna se genera fácilmente mediante inducción magnética en los generadores de AC, diseñados para producir una fem sinusoidal.

# Corriente alterna en una resistencia

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/genrador ac.png">
    <figcaption></figcaption>
    </figure>
</div>


La figura muestra un generador simple de corriente alterna. Un análisis de este tipo de generador se presenta en [[Inducción magnética#Generadores y motores|revisar]] . La fem generada en este sistema viene dada por la ecuación que sigue inmediatamente a la [[Inducción magnética#^59d56c|ecuación]]

$$
\mathcal{E} = \mathcal{E}_{\text{máx}} \cos \omega t \tag{1}
$$

donde $\omega$ es la velocidad angular de la bobina. (La  [[Inducción magnética#^59d56c|ecuación]] presenta la fem proporcional a $\sin \omega t$ en lugar de $\cos \omega t$. La diferencia entre la opción seno y la de coseno está en la elección del origen de tiempos, es decir, cuando $t = 0$.) Si la bobina de $N$ vueltas tiene área $A$, y el campo magnético es uniforme y su módulo es $B$, el máximo de la fem viene dado por $\omega NBA$. Aunque los generadores reales son considerablemente más complicados, todos ellos producen fem sinusoidales, bien por inducción o por movimiento de los circuitos (fem en movimiento). En los diagramas de circuitos, un generador de corriente alterna se representa por el símbolo $\sim$.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/generador ac serie.png">
    <figcaption></figcaption>
    </figure>
</div>

La figura 29.2 muestra un circuito simple de corriente alterna que consiste en un generador ideal y una resistencia. (**Se dice que un generador es ideal si su resistencia interna, su autoinducción y capacitancia o impedancia capacitiva son despreciables**.) 

**La caída de potencial a través de la resistencia $V_R$ es igual a la fem $\mathcal{E}$ del generador**. Si el generador produce una fem dada por la ecuación 1, se tiene que

$$
V_R = V_{R \text{máx}} \cos \omega t
$$

Aplicando la ley de Ohm, tenemos

$$
V_R = IR \tag{2}
$$

Por lo tanto,

$$
V_{R \text{máx}} \cos \omega t = IR \tag{3}
$$

y la corriente en la resistencia es

$$
I = \frac{V_{R \text{máx}}}{R} \cos \omega t = I_{\text{máx}} \cos \omega t \tag{4}
$$

donde

$$
I_{\text{máx}} = \frac{V_{R \text{máx}}}{R} \tag{5}
$$

Obsérvese que la corriente que circula por la resistencia está en fase con la tensión aplicada a la misma, como puede verse en la figura 29.3.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/caida de potencia y corriente en fase.png">
    <figcaption></figcaption>
    </figure>
</div>


La potencia disipada en la resistencia varía con el tiempo. Su valor instantáneo es

$$
P = I^2 R = (I_{\text{máx}} \cos \omega t)^2 R = I_{\text{máx}}^2 R \cos^2 \omega t \tag{6}
$$

En la figura 29.4, puede verse una representación de la potencia en función del tiempo. Varía desde cero hasta su valor máximo $I_{\text{máx}}^2 R$. Normalmente, nos interesa la potencia media a lo largo de uno o más ciclos:

$$
P_m = (I^2 R)_m = I_{\text{máx}}^2 R (\cos^2 \omega t)_m
$$
<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/grafica potencia disipada vs tiempo.png">
    <figcaption></figcaption>
    </figure>
</div>

El valor medio de $\cos^2 \omega t$ en uno o más periodos es $\frac{1}{2}$. Esto puede verse fácilmente a partir de la identidad $\cos^2 \omega t + \sin^2 \omega t = 1$. La representación del $\sin^2 \omega t$ tiene el mismo aspecto que la del $\cos^2 \omega t$, pero está desplazada en $90^\circ$. Ambas tienen el mismo valor medio en uno o más periodos y, como su suma es 1, el valor medio de cada una de ellas debe ser $\frac{1}{2}$. La potencia media disipada en la resistencia es, por lo tanto,

$$
P_m = (I^2 R)_m = \frac{1}{2} I_{\text{máx}}^2 R \tag{7}
$$


## Valores eficaces

### Corriente eficaz
La mayoría de los amperímetros y voltímetros de ac están diseñados para medir **valores eficaces** de la corriente o de la tensión en lugar de los valores máximos o de pico. **Su valor es la raíz cuadrada del valor cuadrático medio respectivo**. Así, el valor eficaz de una corriente es

$$
I_{\text{ef}} = \sqrt{(I^2)_m} \tag{8}
$$

Para una corriente sinusoidal, el valor medio de $I^2$ es

$$
(I^2)_m = [(I_{\text{máx}} \cos \omega t)^2]_m = \frac{1}{2} I_{\text{máx}}^2
$$

Sustituyendo $\frac{1}{2} I_{\text{máx}}^2$ en lugar de $(I^2)_m$ en la ecuación 11, se obtiene

$$
I_{ef} = \frac{1}{\sqrt{2}} I_{max} \approx 0.7071 \ I_{max} \tag{9}
$$

> [!info] El valor eficaz de cualquier magnitud que varía sinusoidalmente con el tiempo es igual al valor máximo de dicha magnitud dividido por $\sqrt{2}$

Sustituyendo  $(I_{max})^2$ en lugar de $\frac{1}{2} I_{max}^2$ en la ecuación 10, se obtiene para la potencia disipada en la resistencia el valor

$$
P_m = (I_{\text{ef}}^2) R \tag{10}
$$

El valor eficaz de la corriente es igual al valor de la corriente continua constante que produciría el mismo calentamiento Joule que la corriente alterna.


### Potencia media suministrada por un generador

Para el circuito sencillo de la  [[generador ac serie.png|figura]]  29.2,  la potencia media aportada por el generador es:

$$
P_m = (\mathcal{E} I)_m = [(\mathcal{E}_{\text{máx}} \cos \omega t)(I_{\text{máx}} \cos \omega t)]_m = \mathcal{E}_{\text{máx}} I_{\text{máx}} (\cos^2 \omega t)_m
$$

o bien,

$$
P_m = \frac{1}{2} \mathcal{E}_{\text{máx}} I_{\text{máx}}
$$

Utilizando $I_{\text{ef}} = I_{\text{máx}} / \sqrt{2}$ y $\mathcal{E}_{\text{ef}} = \mathcal{E}_{\text{máx}} / \sqrt{2}$, puede expresarse así


$$
P_m = \mathcal{E}_{\text{ef}} I_{\text{ef}} \tag{11}
$$


La corriente eficaz está relacionada con la caída de potencial eficaz de la misma forma que la corriente máxima está relacionada con la caída de potencial máxima. Puede verse esto dividiendo cada miembro de la ecuación 5 por $\sqrt{2}$ y utilizando $I_{\text{ef}} = I_{\text{máx}} / \sqrt{2}$ y $V_{\text{ef}} = V_{R \text{máx}} / \sqrt{2}$.

$$
I_{\text{ef}} = \frac{V_{\text{ef}}}{R} \tag{29.12}
$$

Las ecuaciones 10, 11 y 12 tienen la misma forma que las ecuaciones correspondientes a los circuitos de corriente continua, sustituyendo en estas últimas $I$ por $I_{\text{ef}}$ y $V_R$ por $V_{R \text{ef}}$. Así pues, si utilizamos valores eficaces para la corriente y la caída de potencial, podemos calcular la potencia y el calor generado empleando las mismas ecuaciones obtenidas en corriente continua.

> [!info]
> El valor medio de cualquier magnitud en un intervalo de tiempo T es la integral de dicha magnitud en todo ese intervalo dividido por T


# Circuitos de corriente alterna
El comportamiento de la corriente alterna en inductores y condensadores es muy diferente del que se tiene con corriente continua. Por ejemplo, cuando un condensador está en serie en un circuito de cc, la corriente se interrumpe por completo cuando el condensador está totalmente cargado, es decir, actúa como un circuito abierto. Pero si la corriente es alterna, la carga fluye continuamente entrando y saliendo alternativamente de las placas del condensador. Veremos que si la frecuencia de la corriente alterna es alta, un condensador casi no impide la circulación de la corriente, es decir, se comporta como un cortocircuito. Por el contrario, una bobina normalmente tiene una resistencia pequeña $R$, y por lo tanto, es esencialmente un cortocircuito para la corriente continua. Pero cuando la corriente que circula por la bobina está cambiando continuamente, se genera una fuerza contraelectromotriz que es proporcional al ritmo de variación de la corriente, $dI / dt$. Para altas frecuencias, la fuerza contraelectromotriz es grande y el inductor actúa como un circuito abierto.

## Inductores de circuitos de ac

La figura 29.6 muestra una bobina inductora en serie con un generador de corriente alterna. Cuando la corriente crece en el inductor, se crea en éste una fuerza contraelectromotriz de valor $L \, dI / dt$ debido a la variación de flujo. Normalmente, esta fem es mucho mayor que la caída $IR$ debida a la resistencia de la bobina y, por lo tanto, podemos despreciar esta resistencia. La caída de voltaje a través del inductor $V_L$ viene dada entonces por

$$
V_L = L \frac{dI}{dt} \tag{29.13}
$$

**CAÍDA DE POTENCIAL A TRAVÉS DE UN INDUCTOR IDEAL**

En este circuito, la caída de potencial $V_L$ a través del inductor es igual a la fem $\mathcal{E}$ del generador. Esto es,

$$
V_L = \mathcal{E} = \mathcal{E}_{\text{máx}} \cos \omega t = V_{L \text{máx}} \cos \omega t
$$

donde $V_{L \text{máx}} = \mathcal{E}_{\text{máx}}$. Sustituyendo $V_L$ en la ecuación 29.16, se obtiene

$$
V_{L \text{máx}} \cos \omega t = L \frac{dI}{dt} \tag{29.14}
$$

Reordenando, se llega a

$$
dI = \frac{V_{L \text{máx}}}{L} \cos \omega t \, dt \tag{29.15}
$$

El valor de la corriente $I$ se obtiene integrando ambos miembros de esta ecuación:

$$
I = \frac{V_{L \text{máx}}}{L} \int \cos \omega t \, dt = \frac{V_{L \text{máx}}}{\omega L} \sin \omega t + C \tag{29.16}
$$

donde la constante de integración $C$ es la componente de cc de la corriente. Escogiendo la componente de cc de la corriente igual a cero, resulta

$$
I = \frac{V_{L \text{máx}}}{\omega L} \sin \omega t = I_{\text{máx}} \sin \omega t \tag{29.17}
$$

donde

$$
I_{\text{máx}} = \frac{V_{L \text{máx}}}{\omega L} \tag{29.18}
$$

La corriente $I = I_{\text{máx}} \sin \omega t$ está desfasada $90^\circ$ respecto al voltaje a través del inductor, $V_L = V_{L \text{máx}} \cos \omega t$. En la figura 29.7, que muestra $I$ y $V_L$ en función del tiempo, podemos ver que el valor máximo del voltaje ocurre $90^\circ$ (o sea, un cuarto de periodo) antes que el correspondiente valor máximo de la corriente. Se dice que la caída de voltaje a través del inductor adelanta a la corriente en $90^\circ$. Podemos comprender esto físicamente. Cuando $I$ es cero, pero está decreciendo, $dI / dt$ es mínimo, de modo que la fem inducida por la bobina $V_L$ pasa por un valor máximo. Un cuarto de ciclo después, $I$ es máximo. En ese momento, $dI / dt$ es cero, de modo que $V_L$ es cero. Usando la identidad trigonométrica $\sin \theta = \cos (\theta - \pi / 2)$, donde $\theta = \omega t$, la ecuación 29.17 puede expresarse como

$$
I = I_{\text{máx}} \cos (\omega t - \frac{\pi}{2}) \tag{29.19}
$$

La relación entre la corriente máxima (o eficaz) y la tensión máxima (o eficaz) en el caso de una bobina, puede expresarse de una forma semejante a la ecuación 29.12 correspondiente a una resistencia. A partir de la ecuación 29.18, tenemos

$$
I_{\text{máx}} = \frac{V_{L \text{máx}}}{\omega L} = \frac{V_{L \text{máx}}}{X_L} \tag{29.20}
$$

donde

$$
X_L = \omega L \tag{29.21}
$$

**DEFINICIÓN: REACTANCIA O IMPEDANCIA INDUCTIVA**




![[Pasted image 20240704161251.png]]

![[Pasted image 20240704161306.png]]


![[Pasted image 20240704161320.png]]











<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/.png">
    <figcaption></figcaption>
    </figure>
</div>





<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/.png">
    <figcaption></figcaption>
    </figure>
</div>





<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/.png">
    <figcaption></figcaption>
    </figure>
</div>




<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/.png">
    <figcaption></figcaption>
    </figure>
</div>