Las fem y las corrientes causadas por los flujos magnéticos variables se denominan **fem inducidas** y **corrientes inducidas**. En sí mismo, el proceso se denomina **inducción magnética**. Una fem producida cuando un conductor se mueve en una región en la que existe campo magnético se denomina **fem de movimiento**.


# Flujo magnético
El flujo magnético $\phi_m$ se define por la expresión
$$
\phi_m = \int_S \vec{B} \cdot \hat{n} \ dA = \int_S B_n \ dA
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
\phi_m = NBAcos(\theta)
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
\xi = - \frac{d\phi_m}{dt}
$$
El signo negativo se debe al sentido de la fem inducida.

## Fem inducida en un circuito estacionario en un campo magnético variable
Los campos eléctricos que hemos estudiado previamente eran el resultado de cargas eléctricas estáticas. Estos campos son conservativos, lo cual significa que  su circulación alrededor de una curca cerrada $C$ es cero. (Se define la circulación del potencial vector $\vec{E}$ alrededor de la curva $C$ como $\oint \vec{E} \cdot d\vec{l}$). Sin embargo, el campo eléctrico resultante de un flujo magnético variable **no es conservativo**. La circulación alrededor de $C$ es una fem inducida igual a la variación con el tiempo del flujo magnético a través de cualquier superficie $S$ encerrada por $C$ cambiada de signo
$$
\xi = \oint_C \vec{E}_{nc} \cdot d\vec{l} = - \frac{d}{dt} \int_S \vec{B} \cdot \hat{n} dA = -\frac{d\phi_m}{dt}
$$

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/fem inducida espira.png" alt="Induccion por conexión a tierra" width=400>
    <figcaption></figcaption>
    </figure>
</div>


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>



<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
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
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>



> [!info] Formulación alternativa de la ley de Lenz
> Cuando se produce una variación del flujo magnético que atraviesa una superficie, el campo magnético debido a la corriente inducida genera un flujo magnético sobre la misma superficie que se opone a dicha variación.


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>




# Fem de movimiento

>[!info] Definición
>Fem de movimiento es toda fem inducida por el movimiento de un conductor en un campo magnético

## Carga total a través de una bobina que gira


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>



## Generadores y motores


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>


# Inductancia




<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>




<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>


# Energía magnética


<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>


# Circuitos RL



<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/">
    <figcaption></figcaption>
    </figure>
</div>
