

# Corriente y movimiento de cargas
![[Pasted image 20240510105212.png]]

![[Pasted image 20240510105310.png]]

La intensidad de la corriente es, por lo tanto
## Relación entre la intensidad y la velocidad de desplazamiento
$$ I = \frac{\Delta Q}{\Delta t} = qnAv_d $$

## Densidad de corriente
La corriente por unidad de área es $qnv_d$, el vector **densidad de corriente, $\vec{J}$** viene dado por la siguiente expresión
$$ \vec{J} = qn\vec{v_d} $$

## Definición de corriente
La corriente a través de la superficie $S$ se define como el flujo del vector densidad de corriente $\vec{J}$ a través de la superficie, esto es
$$ I = \int_S \vec{J} \cdot d\vec{A} = \int_S \vec{J} \cdot \vec{n} \,dA $$
donde $d\vec{A}$ es un elemento de área multiplicado por el vector unitario $\vec{n}$ que es perpendicular a la superficie $S$ en el punto donde se ubica dicho elemento de área.

![[Pasted image 20240510121637.png]]



# Resistencia y Ley de Ohm
![[Pasted image 20240510110121.png]]
El cociente entre la caída de potencial en la dirección de la corriente y la intensidad de la corriente se llama **resistencia** del segmento

## Resistencia
$$  R = \frac{V}{I} $$
La unidad de la resistencia es el **ohm** $\Omega$, $1 \Omega = 1 \, V/A$
![[Pasted image 20240510110133.png]]

## Ley de Ohm
![[Pasted image 20240510110444.png]]
$$ V = IR $$
![[Pasted image 20240510110530.png]]


## Resistividad de un material
La resistencia de un alambre conductor es proporcional a su longitud $L$ e inversamente proporcional a su área transversal $A$
$$ R = \rho \frac{L}{A} $$
siendo $\rho$ una constante de proporcionalidad denominada **resistividad del material conductor**
Su unidad es el *ohm-metro* ($\Omega \cdot m$)


![[Pasted image 20240510123739.png]]


# Energía en los circuitos eléctricos
El mecanismo por el cual el incremento de energía interna de un conductor da lugar a un aumento de su temperatura se denomina **efecto Joule**.
![[Pasted image 20240510111416.png]]


![[Pasted image 20240510111402.png]]
$$ \Delta U = \Delta Q(V_b - V_a) $$
Como $V_a >V_b$ esto supone una pérdida neta en la energía potencial de $Q$. La energía perdida es, por tanto, 
$$ - \Delta U = \Delta QV $$
donde $V = V_a - V_b$ es la caída del potencial de un lado a otro del segmento. La variación temporal de la pérdida de energía potencial es
$$ -\frac{\Delta U}{\Delta t} = \frac{\Delta Q}{\Delta t}V$$
Haciendo el límite cuando $\Delta t$ tiende a cero, se obtiene
$$ - \frac{dU}{dt} = \frac{dQ}{dt}V = IV $$

## Potencia disipada en un conductor por unidad de tiempo
La energía perdida por unidad de tiempo es la potencia $P$ disipada en el segmento del conductor, que a su vez, es la velocidad con la que se disipa a energía potencial eléctrica en dicho segmento
$$ P = IV $$

## Potencia disipada en una resistencia
En un conductor, la energía potencial se disipa como energía térmica, utilizando $V = IR$ la ecuación puede expresarse en otras formas útiles
$$ P = IV = I^2R = \frac{V^2}{R} $$

![[Pasted image 20240510112236.png]]

![[Pasted image 20240510112134.png]]
## Potencia suministrada por una fuente de FEM
$$ P = \frac{(\Delta Q) \xi}{\Delta t} = I \xi $$


# Asociaciones de resistencias

## Resistencias en serie
Cuando dos o más resistencias están conectadas de modo que a través de ellas circula la misma corriente $I$, se dice que las resistencias están conectadas en serie.
**Resistencia equivalente a $n$ resistencias en serie**

$$  R_{eq} = \sum_{i=1}^n R_i $$

## Resistencias en paralelo
Dos resistencias conectadas de modo que a través de ellas existe la misma diferencia de potencial, se dice que están conectadas en paralelo.

**Resistencia equivalente a $n$ resistencias en paralelo**

$$   \frac{1}{R_{eq}} = \sum_{i=1}^n \frac{1}{R_i}   $$



# Reglas de Kirchhoff

> 1. La suma algebraica de las variaciones de potencial a lo largo de cualquier bucle o malla del circuito debe ser igual a cero.
> 2. En un punto o nudo de ramificación de un circuito en donde puede dividirse la corriente, la suma de las corrientes que entran en el nudo debe ser igual a la suma de las corrientes que salen del mismo




![[Pasted image 20240510104859.png]]
![[Pasted image 20240510104958.png]]
![[Pasted image 20240510105022.png]]

