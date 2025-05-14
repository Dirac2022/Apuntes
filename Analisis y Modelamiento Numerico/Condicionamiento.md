Decimos que un proceso numérico es estable si errores pequeños producidos en una etapa del proceso se magnifican en las etapas subsecuentes y degradan seriamente la exactitud del calculo general.

## Inestabilidad numérica
Informalmente decimos que un proceso numérico es **inestable** si pequeños errores cometidos en un etapa del proceso son magnificados en etapas posteriores y degradan seriamente la exactitud del cálculo general.


## Condicionamiento
Nos indica que tan sensible la solución de un problema puede ser para cambios  relativos pequeños en los datos de entrada. Un problema esta **mal condicionado** si pequeños errores en la data puede producir grandes cambios en la respuesta.

### Numero de condición de una función
Supongamos que nuestro problema es simplemente evaluar una función $f$ en el punto $x$. ¿Cuál es el efecto en $f(x)$ si perturbamos $x$?. Podemos usar el *teorema del valor medio*
$$ f(x + h) - f(x) = f'(c)h \approx hf'(x) $$
Por tanto, si $f'(x)$ no es muy grande, el efecto en la perturbación en $f(x)$ es pequeño.

Sin embargo, es el **error relativo** es el que es significativo en tales cuestiones. Si perturbamos $x$ una cantidad $h$, tenemos $h/x$ como **el tamaño relativo de la perturbación**. Del mismo modo, cuando $f(x)$ es perturbado a $f(x+h)$, el tamaño relativo de esa perturbación es
$$ \frac{f(x+h) - f(x)}{f(x)} \approx \frac{hf'(x)}{f(x)} = \left[ \frac{xf'(x)}{f(x)} \right] \left(\frac{h}{x} \right) $$
Así, el factor $xf'(x) / f(x)$ sirve como **numero de condición** para este problema.


## Numero de condición de una matriz $\kappa$(A)

Consideremos el sistema $Ax = b$, de solución $u$. Queremos controlar qué cambios
se producen en la solución cuando hacemos pequeños cambios en las componentes de
$b$ o de $A$. Empecemos por tomar un cambio $\Delta b$ en $b$. Entonces la solución cambiará a
$u + \Delta u$, y se tiene
$$A(u + \Delta u) = b + \Delta b \: , \quad A\Delta u = \Delta b $$
Por tanto, el cambio en la solución se estima en $A^{-1}\Delta b$. Si tomamos una norma vectorial
y la norma matricial subordinada, entonces
$$ \|\Delta u\| \leq \|A^{-1}\| \|\Delta b\| $$
Por otro lado, $\|b\| \leq \|A\| \|u\|$, de donde $\frac{1}{\|u\|} \leq \frac{\|A\|}{\|b\|}$. Medimos el error relativo, y
obtenemos
$$ \frac{\|\Delta u\|}{\|u\|} \leq \|A\|\|A^{-1}\| \frac{\|\Delta b\|}{\|b\|} $$
Así, la variación en el error relativo de la solución está asociada a la cantidad $\|A\| \|A^{-1}\|$. 


**Definición**
Sea $\|\cdot \|$ una norma matricial subordinada y $A$ una matriz **inversible**, entonces el número 
$$ \kappa(A) = cond(A) = \|A\|\|A^{-1}\| $$
se denomina **numero de condición** o condicionamiento de la matriz $A$ respecto a $\| \cdot\|$

*No hay problema en extender la definición a cualquier norma matricial.*

Si solución de $Ax = b$ es bastante insensible a pequeños cambios en el lado derecho, $b$, entonces pequeñas perturbaciones en $b$ resultan en solo pequeñas perturbaciones en la solución calculada $x$. En este caso se dice que $A$ esta **bien condicionada**. Por el contrario si $\kappa(A)$ es grande, entonces $A$ esta **mal condicionada**.




## Teorema
Sea $\|\cdot \|$ una normal matricial *subordinada*, $A$ matriz inversible y $b \neq 0$. Si 
$$ Au = b \: , (A + \Delta A)(u + \Delta u) = b $$
entonces
$$ \frac{\|\Delta u\|}{\|u + \Delta u\|} \neq cond(A) \frac{\|\Delta  A\|}{A} $$

## Teorema
Sea $\|\cdot \|$ una normal matricial *subordinada*, $A$ matriz inversible y $\|\Delta A\| < 1 / \|A^{-1} \|$. Si

$$ (A + \Delta A)(u + \Delta u) = b + \Delta b $$

entonces
$$ \frac{\|\Delta u\|}{u} \neq \frac{cond(A)}{1-cond(A)\frac{\|\Delta  A\|}{\|A\|}}    \left ( \frac{\|\Delta  b\|}{b} + \frac{\|\Delta  A\|}{\|A\|} \right ) $$

## Proposicion
Sea $\|\cdot \|$ una normal matricial *subordinada*, $A$ matriz inversible, entonces

1. $cond(A) \geq 1$
2. $cond(A) = cond(A^{-1})$
3. $cond(\lambda A) = cond(A) \: \forall \lambda \in \mathbb{K} - \{0\}$


# Condición de una matriz
Sea $A = (a_{ij})$ una matriz de $m$ por $n$, se le llama *numero de condición* a $k(A)$ o $Cond(A)$ tal que $$Cond(A) = ||A|| \dot ||A^{-1}||$$
Donde $||A||$ es una [[Norma matricial]]
- La matriz se dice *bien condicionada* si su *numero de condición* esta cerca de **1**.
- Se dice *mal condicionada* si es significativamente mayor que **1**, esto nos indicaría que pequeñas variaciones en los datos pueden producir grandes variaciones en los resultados y por tanto que la solución del sistema es propensa a grandes errores de redondeo.
