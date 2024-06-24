

El potencial de un único conductor aislado, que contiene una carga $Q$ es proporcional a esta carga y depende del tamaño y forma del conductor


# Capacidad


Un condensador es un dispositivo constituido por dos conductores, uno de ellos cargado con carga $Q$ y el otro con carga $-Q$. La relación entre la carga $Q$ y la diferencia de potencial existente entre los dos conductores se define como **capacidad del condensador**.

## Definición de capacidad
$$ C = \frac{Q}{V}  $$
![[Pasted image 20240502164022.png]]
$$ 1 \: F = 1 \: C / \: V $$
### Constante eléctrica
$$ \epsilon_0 = 8.85 \times 10^{-12} F/m = 8.85 pF/m  $$
## Condensadores
Un sistema de dos conductores portadores de cargas iguales y opuestas constituye un condensador. 
![[Pasted image 20240502164533.png]]


## Condensadores de placas paralelas

Esta formado por dos grandes placas conductoras paralelas. Sea $A$ el área de cada placa y $d$ la distancia de separación. Situamos una carga $+Q$ en una placa y $-Q$ en la otra. Como las placas están muy próximas, el campo en cualquier punto situado entre ellas es, aproximadamente, igual al campo debido a dos planos infinitos con cargas iguales y opuestas. Cada placa contribuye con un campo uniforme de modulo $E=\sigma / (2\epsilon_0)$. Resultando así un campo total $E = \sigma / \epsilon_0$ donde $\sigma = Q/A$. 

Como el campo que existe entre las placas de este condensador es uniforme.
![[Pasted image 20240502165500.png]]
la diferencia de potencial entre las placas es igual al campo $\vec{E}$ multiplicado por la separación de las placas $d$
![[Pasted image 20240502165558.png]]
Vemos que la capacidad no depende ni de $Q$ ni de $V$.
En general, la capacidad depende del tamaño, forma, geometría y posición relativa de los conductores y también de las propiedades del medio aislante que los separa.



## Condensadores cilíndricos
Un condensador cilíndrico consta de un pequeño cilindro o alambre conductor de radio $R_1$ y una corteza cilíndrica mayor de radio $R_2$ concéntrica con la anterior. De longitud L
![[Pasted image 20240502184610.png]]
$$
C = \frac{Q}{V} = \frac{2\pi\varepsilon_0 L}{ln(R_2 / R_1)}
$$




# Almacenamiento de la energía eléctrica
Consideremos inicialmente dos conductores descargados que no están en contacto entre sí. Sea $q$ la carga transferida al cabo de cierto tiempo durante el proceso de cargar el condensador. La diferencia de potencial es entonces $V = q/C$. Si se transfiere ahora una pequeña cantidad adicional de carga $dq$ desde el conductor negativo a potencial cero hasta el conductor positivo a un potencial $V$ la energía potencial del condensador se incrementa en 
$$ dU = Vdq = \frac{q}{C}dq $$
Integrando desde $0$ hasta su valor final $Q$
$$ U = \int_0^Q \frac{q}{C}dq = \frac{1}{2}\frac{Q^2}{C} $$
## Energía potencial almacenada en un condensador
> $$ U = \frac{Q^2}{2} = \frac{QV}{2} = \frac{CV^2}{2} $$


## Energía del campo electrostático
Es posible relacionar la energía almacenada en el condensador con el campo eléctrico $E$ existente entre las placas.
- $V = Ed$, donde $d$ es la separación entre las placas
- $C = \varepsilon A/d$

Entonces la energía almacenada se puede expresar como
$$ U = \frac{CV^2}{2} = \frac{1}{2} \left(\frac{\varepsilon_0A}{d}\right)(Ed)^2 = \frac{1}{2}\varepsilon_0 E^2 (Ad) $$
donde $Ad$ es el volumen que encierra las placas paralelas del condensador que contiene el campo eléctrico. La energía por unidad de volumen se denomina densidad de energía $u_e$

### Densidad de energía de un campo electrostático
>$$u_e = \frac{1}{2}\varepsilon_0 E^2$$

**Siempre que exista un campo eléctrico en el espacio, la energía electrostática por unidad de volumen viene dada por la ecuación anterior**

## Asociación de condensadores

### Condensadores en paralelo
Los dispositivos que se conectan en paralelo comparten la misma diferencia de potencial entre sus respectivos extremos debido únicamente al modo en que están conectados.
**La capacidad equivalente de $n$ condensadores en paralelo es**
$$ C_{eq} = \sum_{i=1}^n C_i$$

### Condensadores en serie
Cuando un conjunto de condensadores están conectados de tal forma que una placa de u condensador de conecta a otra mediante un cable *sin nudos*, es decir, sin puntos donde un cable se divide en dos o más cables, se dice que esta disposición esta en serie.
**La capacidad equivalente de $n$ condensadores en serie es**
$$  \frac{1}{C_{eq}} = \sum_{i=1}^n \frac{1}{C_i} $$



# Dieléctricos
Cuando el espacio entre los dos conductores de un condensador se ve ocupado por un dieléctrico, la capacidad aumenta en un factor $\kappa$ que es característico del dieléctrico.
Sea un condensador cargado, aislado y sin dieléctrico. Se introduce un dieléctrico, entonces el campo en el interior del dieléctrico introducido entre las placas es
$$ E = \frac{E_0}{\kappa} $$
donde $E_0$ es el campo original sin dieléctrico.

## Efecto de un dieléctrico sobre la capacidad
Como $C=Q/V$, se obtiene que la nueva capacidad cuando se introduce un dieléctrico a un condensador es
$$ C = \kappa C_0 $$
donde $C_0$ es la capacidad inicial sin dieléctrico.
La capacidad de un condensador de placas paralelas lleno de un material dieléctrico de constante $\kappa$ es, por tanto
$$ C = \frac{\kappa \varepsilon_0 A}{d} = \frac{\varepsilon A}{d} $$
donde $\varepsilon = \kappa \varepsilon_0$ es la **permitividad del dieléctrico**.

## Energía almacenada en presencia de un dieléctrico
De la [[#Energía potencial almacenada en un condensador|ecuación]] anterior, podemos expresar la energía almacenada como
$$  U = \frac{CV^2}{2} = \frac{1}{2} \left(\frac{\varepsilon A}{d}\right)(Ed)^2 = \frac{1}{2}\varepsilon E^2 (Ad)  $$
donde $Ad$ es el volumen entre las placas. La energía por unidad de volumen es, por lo tanto, 
$$ u_e = \frac{1}{2}\varepsilon E^2 = \frac{1}{2}\kappa \varepsilon_0 E^2 $$
Parte de esta energía es la asociada con el campo eléctrico y el resto es la energía **procedente de la polarización del dieléctrico**.

![[Pasted image 20240510104720.png]]
![[Pasted image 20240510104738.png]]
![[Pasted image 20240510104753.png]]



