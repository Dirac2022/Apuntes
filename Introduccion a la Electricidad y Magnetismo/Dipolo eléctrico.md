

# Dipolo eléctrico
Un sistema de dos cargas iguales y opuestas $q$ separadas por una pequeña distancia $L$ se denomina **dipolo eléctrico**.
## Momento dipolar eléctrico
$$ \vec{p} = q \vec{L} $$
donde $L$ es el vector que va desde la carga negativa hacia la positiva.
El **campo** creado por el dipolo en el eje del dipolo, **en un punto alejado**.
$$ |E| = k \frac{2p}{r^3}  $$



# Dipolos eléctricos en campos eléctricos
Ciertas moléculas poseen momentos dipolares eléctricos permanentes debido a una distribución no uniforme de carga dentro de la molécula. Tales moléculas se llaman **moléculas polares**.

Un campo eléctrico externo uniforme no ejerce una fuerza neta sobre un dipolo pero aparece un par de fuerzas que tiende a alinear el dipolo en la dirección del campo.

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/dipolo en campo electrico uniforme.png" alt="Dipolo en campo eléctrico uniforme">
    <figcaption>Dipolo en campo eléctrico uniforme</figcaption>
    </figure>
</div>
El momento de las fuerzas ejercidas sobre las cargas es
$$ 
\begin{aligned}
\tau &= \vec{L} \times \vec{F} \\
	&= \vec{L} \times q\vec{E} \\
	&= q \vec{L} \times \vec{E} \\
\tau	&= \vec{p} \times \vec{E} \\
\end{aligned}
$$


Cuando un dipolo gira un ángulo $d\theta$, el campo eléctrico realiza un trabajo
$$ dW = - \tau d\theta = - pEsen\theta d\theta$$
El signo menos es debido a que el momento tiende a disminuir $\theta$. Igualando este trabajo con la disminución de energía potencial, resulta
$$ dU = -DW = pEsen\theta d\theta$$
Integrando y tomando como cero de energía potencial la que corresponde a $\theta = 90°$, obtenemos la siguiente expresión
## Energía potencial de un dipolo en un campo externo
$$ U = -pEcos\theta = -\vec{p} \cdot \vec{E} $$

## Moléculas no polares
Las moléculas no polares no poseen momento dipolar eléctrico permanente. Sin embargo, todas las moléculas neutras contienen cantidades iguales de carga positiva y negativa. En presencia de un campo eléctrico externo $\vec{E}$, las cargas se separan espacialmente. Las cargas positivas se mueven en dirección de $\vec{E}$ y las negativas en dirección opuesta. La molécula adquiere de este modo un momento dipolar inducido paralelo al campo eléctrico externo y se dice entonces que está **polarizada**.

# Polarización en dieléctricos
Para comprender el efecto macroscópico de un campo eléctrico en **dieléctrico** consideremos un átomo del dieléctrico, compuesto por una carga negativa $-Q$ (nube de electrones) y una carga positiva $+Q$ (núcleo). Una molécula del dieléctrico podría describirse de la misma manera. Al aplicarse un campo eléctrico $\vec{E}$, la carga positiva es desplazada por la fuerza $\vec{F}_+ = Q\vec{E}$ desde su posición de equilibrio hacia la dirección de $\vec{E}$, en tanto que la carga negativa es desplazada en dirección opuesta por la fuerza $\vec{F}_- = Q\vec{E}$ . En razón del desplazamiento de las cargas resulta un dipolo, se dice que el dieléctrico ha sido **polarizado**. En el estado polarizado, el campo eléctrico $\vec{E}$ aplicado distorsiona la nube de electrones. Esta distribución distorsionada de carga equivale, en virtud del principio de superposición, a la distribución original más un dipolo cuyo momento es
$$ \vec{p} = Q \vec{d} $$
donde $\vec{D}$ es el vector distancia de $-Q$ a $+Q$ del dipolo.
![[Pasted image 20240509231532.png]]
Si hay $n$ dipolos en un volumen $\Delta_v$ del dieléctrico, el momento del dipolo total debido al campo eléctrico es
$$ \sum_{i=1}^n Q_i \vec{d}_i $$
La polarización $\vec{P}$ ($C/m^2$) es el momento del dipolo por unidad de volumen del dieléctrico, es decir,

$$ \vec{P} = \lim_{\Delta v \to 0} \dfrac{\sum_{i=0}^n Q_i \vec{d}_i}{\Delta v} $$
El principal efecto del campo eléctrico $vec{E}$ sobre un dieléctrico es la creación de momentos del dipolo que se alinean en la dirección de $vec{E}$.