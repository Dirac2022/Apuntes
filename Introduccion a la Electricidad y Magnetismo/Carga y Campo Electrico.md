
# Carga eléctrica

- La carga eléctrica es una propiedad intrínseca de muchas partículas elementales. La masa es otra propiedad intrínseca de muchas de ellas. - https://www.youtube.com/watch?v=Gc2WtxNS3U0
- La carga siempre está conectada a la masa (relación e/m).
- No todas las partículas elementales tienen carga.
- La masa está asociada a la interacción gravitacional, la carga a la interacción electromagnética.
- Al mismo tiempo, la masa tiene la propiedad de inercia, tiene carga.
- Hay dos tipos de cargas opuestas: positivas y negativas.
- La carga está "*cuantificada*", es decir, ocurre solo en múltiplos enteros de una carga elemental.

**La unidad de la carga es el Coulomb (C).**
## Carga elemental
$$e^- = 1.602 176 53(14) \times 10^{-19}C$$
$$ e^- \approx 1.602 \times 10^{-19} $$


Las partículas elementales con carga que son relevantes en átomos y moléculas son electrones ( de carga $Q_e = -e$) y los protones ($Q_p =+e$).
Se ha verificado experimentalmente que la carga electrones y protones se diferencia en menos $10^{-20}e$.

## Ley de la Conservación:
**En un sistema cerrado la carga total se conserva.**

Pares de cargas ($+e$ / $-e$) pueden ser creadas o aniquiladas.
Esto ocurre p. ej. mediante la creación de pares electrón/positrón en la que se transforma la energía en masa / antimasa.(Ver https://es.wikipedia.org/wiki/Antimateria)

# Fuerza entre cargas
Las cargas con diferentes signos se atraen, con mismo signo se repelen. Se observa que la fuerza entre dos cargas $Q_1$ y $Q_2$ a una distancia $r$ se cumple:
$$ F \propto \frac{Q_1 \cdot Q_2}{r^2}$$
La fuerza sobre la carga $Q_2$ actúa en dirección del vector distancia $r$, que va desde la carga $Q_1$ hacia $Q_2$
 $$\vec{F} \propto \frac{Q_1 \cdot Q_2}{|\vec{r}|^2} \frac{\vec{r}}{|\vec{r}|}$$

<div style="text-align: center;">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSdxqmnWbTyiHg8Rf9M4SUwv8AMksHXs9XKs8_IQy34IQ&s" alt="Texto alternativo de la imagen">
</div>


## Ley de Coulomb

$$ F = \frac{1}{4\pi\varepsilon_0} \frac{Q_1  Q_2}{R^2}$$

### Constante dieléctrica del vacío
$$ \varepsilon_0 = 8.854187817 ... \times 10^{-12} C^2 / (Nm^2)$$

Entonces, la constante de proporcionalidad $1/4\pi\varepsilon_0$ equivale a 
$$ \frac{1}{4\pi\varepsilon_0} = 8.988 \cdot 10^9 Nm^2 / C^2$$
### Ley de Coulomb en forma vectorial
Si una carga $q_1$ se encuentra en la posición $\vec{r}_1$ y $q_2$ en $\vec{r}_2$, la fuerza $\vec{F}_{12}$ ejercida por $q_1$ sobre $q_2$ es
$$ \vec{F}_{12} = \frac{1}{4\pi\varepsilon}_0 \frac{q_1q_2}{r^2_{12}} \hat{r}_{12}  $$
donde $\hat{r}_{12}$ es un vector unitario que apunta de $q_1$ a $q_2$.


### Fuerza ejercida por un sistema de cargas
En un sistema de cargas, cada una de ellas ejerce una fuerza dada por la ecuación anterior. Así, la fuerza neta sobre cada carga es la suma vectorial de las fuerzas individuales ejercidas sobre dicha carga por las restantes cargas del sistema.

# El campo eléctrico $\vec{E}$
Una carga crea un campo eléctrico $\vec{E}$ en todo el espacio y este campo ejerce una fuerza sobre cada carga alrededor. Los cambios del campo se propagan a través del espacio con la velocidad de la luz $c$. Si una carga se mueve súbitamente, la fuerza que ejerce sobre otra carga a la distancia $r$ no se modifica hasta que transcurre el tiempo $r / c$.

1. La interacción (fuerza) entre dos cargas se puede imaginar como una acción a distancia sobre una gran distancia.
2. Otra idea es utilizar el término "campo".

- Una carga crea un campo eléctrico y la otra carga experimenta una fuerza en el campo.
- Los campos son algo real porque en ellos se almacena energía.
- Hay campos que se han desprendido de la carga generadora y transportan energía (ondas electromagnéticas).
- Otras cargas pueden experimentar fuerzas en estos campos. Esto no podría explicarse por un efecto a distancia.

Se va a introducir el concepto de **campo eléctrico** mediante una carga $q$ que experimenta la fuerza $\vec{F} = q \vec{E}$, donde $\vec{E}$ es la intensidad de campo eléctrico.

De la [[#Ley de Coulomb]] se obtiene la fuerza sober la carga $q$ en el punto $\vec{r}$  a través del campo generado por la carga $Q$
$$ F = \frac{1}{4\pi\varepsilon_0} \frac{Q  q}{r^2} = E q $$
Esto es,
$$ E = \frac{1}{4\pi\varepsilon_0} \frac{Q}{r^2} $$
Escrito en forma vectorial           

$$ \vec{E} = \frac{1}{4\pi\varepsilon_0} \frac{Q}{|\vec{r}|^2} \frac{\vec{r}}{|\vec{r}|} = \frac{1}{4\pi\varepsilon_0} \frac{Q}{|\vec{r}|^2} \hat{r}$$

Una carga $Q$ en la ubicación $\vec{r_1}$ genera un campo eléctrico de la forma
$$ \vec{E}(\vec{r}) = \frac{1}{4\pi\varepsilon_0} \frac{Q}{|\vec{r_2} - \vec{r_1}|^2} \frac{\vec{r_2} - \vec{r_1}}{|\vec{r_2} - \vec{r_1}|} $$

La dirección del campo se invierte si la carga $Q$ es negativa.


## Principio de superposición
Si hay varias cargas en el espacio, las contribuciones de cada carga se suman vectorialmente (*principio de superposición*) a la intensidad del campo eléctrico. Las tres cargas $Q_1$, $Q_2$, y $Q_3$ en las ubicaciones $r_1$, $r_2$ y $r_3$ generan el campo:

$$ \vec{E}(\vec{r}) = 
\frac{1}{4\pi\varepsilon_0} \frac{Q_1}{|\vec{r} - \vec{r_1}|^2} \frac{\vec{r} - \vec{r_1}}{|\vec{r} - \vec{r_1}|} + 
\frac{1}{4\pi\varepsilon_0} \frac{Q_2}{|\vec{r} - \vec{r_2}|^2} \frac{\vec{r} - \vec{r_2}}{|\vec{r} - \vec{r_2}|} +
\frac{1}{4\pi\varepsilon_0} \frac{Q_3}{|\vec{r} - \vec{r_3}|^2} \frac{\vec{r} - \vec{r_3}}{|\vec{r} - \vec{r_3}|} $$

Para $n$ cargas se puede escribir:

$$ \vec{E}(\vec{r}) = \sum_{i=1}^n \frac{1}{4\pi\varepsilon_0} \frac{Q_i}{|\vec{r} - \vec{r_i}|^2} \frac{\vec{r} - \vec{r_i}}{|\vec{r} - \vec{r_i}|}$$
### Campo eléctrico $\vec{E}$ debido a un sistema de cargas puntuales
$$ \vec{E}_p = \sum_i \vec{E}_{ip} $$
<div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Camposcargas.svg/1118px-Camposcargas.svg.png">
    <figcaption>Lineas de campo electrico</figcaption>
</div>



<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Resumen1-carga-campo.png" alt="">
    <figcaption>Resumen 1</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Resumen2-carga-campo.png" alt="">
    <figcaption>Resumen 2</figcaption>
    </figure>
</div>

<div style="text-align: center;">
	<figure>
    <img src="C:/Users/mitch/OneDrive - UNIVERSIDAD NACIONAL DE INGENIERIA/Mi unidad/My Notes/My Notes/Introduccion a la Electricidad y Magnetismo/imgs/Resumen3-carga-campo.png" alt="">
    <figcaption>Resumen 3</figcaption>
    </figure>
</div>
