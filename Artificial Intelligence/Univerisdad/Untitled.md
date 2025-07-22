
Perfecto. Voy a preparar una explicación detallada y rigurosa de las primeras 10 preguntas del documento, como si fueran clases teóricas. Incluiré fundamentos matemáticos completos, derivaciones paso a paso, y usaré analogías físicas e ilustraciones solo cuando sean realmente necesarias para la comprensión conceptual. Te avisaré en cuanto esté listo.

# Máquinas de Boltzmann: Respuestas a las preguntas 1–10

## Pregunta 1: Función de energía de una BM no restringida y distribución de probabilidad

Una **máquina de Boltzmann (BM)** general está formada por _unidades binarias_ (visibles y ocultas) conectadas entre sí de forma arbitraria. A cada configuración de estados $s=(v,h)$ (vector de visibles $v$ y de ocultos $h$) se le asigna una **energía** definida como la suma de interacciones binarias y términos de sesgo. En una formulación habitual, si llamamos $s_i\in{0,1}$ al estado de la unidad $i$, la energía puede escribirse como

$$
E(s) = -\sum_{i<j} w_{ij}\,s_i\,s_j - \sum_i b_i\,s_i
$$

donde $w_{ij}=w_{ji}$ son los **pesos** de la conexión entre las unidades $i,j$ (pueden ser visibles-visibles, visibles-ocultas u ocultas-ocultas en la BM general) y $b_i$ son **sesgos** locales. Esta expresión incluye todas las interacciones bilineales posibles sin restricción (por eso “BM no restringida”).

En analogía con la mecánica estadística, la BM define una distribución de probabilidad Boltzmann sobre configuraciones por medio de la **función de partición** $Z$:

$$
p(s) = \frac{1}{Z} \exp(-E(s)), \quad Z = \sum_s \exp(-E(s))
$$

Esto garantiza que $\sum_s p(s)=1$. Así, la distribución conjunta de visibles y ocultos está dada por

$$
p(v,h) = \frac{\exp(-E(v,h))}{Z}
$$

La probabilidad de una configuración visible $v$ se obtiene sumando sobre los posibles $h$ ocultos. Esta distribución es la **distribución de Boltzmann** asociada a la energía definida, y el factor $Z$ normaliza la probabilidad.

_Derivación detallada._ Partimos de definir la energía de un estado $s$. Para cada par de unidades $i<j$ con conexión $w_{ij}$, contribuye $-w_{ij}s_i s_j$, y cada unidad $i$ con sesgo $b_i$ aporta $-b_i s_i$. Con ello, la probabilidad conjunta es proporcional a $\exp(-E(s))$, y exigiendo que sume 1 se introduce la función de partición $Z=\sum_s \exp(-E(s))$. Por lo tanto,

$$p(v,h)=\frac{1}{Z}\exp\Bigl(\sum_{i<j} w_{ij}s_i s_j + \sum_i b_i s_i\Bigr),$$

que coincide con la forma $p(s)=\exp(-E(s))/Z$.

## Pregunta 2: Intractabilidad del gradiente de log-verosimilitud

Para entrenar una BM se suele maximizar la **log-verosimilitud** de los datos bajo el modelo. Si ${v^{(n)}}$ es el conjunto de datos de $N$ vectores visibles, la log-verosimilitud total es

$$\mathcal{L}(W,b) = \sum_{n=1}^N \log p(v^{(n)};W,b),$$

donde $p(v)=\sum_h p(v,h)$. Diferenciar respecto a un peso $w_{ij}$ se puede derivar (usando la forma de $p(v,h)$) que la pendiente (gradiente) es la diferencia de dos expectativas:

\frac{\partial \mathcal{L}}{\partial w_{ij}} \;=\; \underbrace{\mathbb{E}_{\text{datos}}\bigl[s_i s_j\bigr]}_{\text{f_ datos}} \;-\; \underbrace{\mathbb{E}_{\text{modelo}}\bigl[s_i s_j\bigr]}_{\text{f_modelo}}.

Aquí, $\mathbb{E}_{\text{datos}}[s_i s_j]$ se puede calcular directamente de los datos (fase positiva), pero $\mathbb{E}_{\text{modelo}}[s_i s_j]$ exige promediar $s_i s_j$ sobre la _distribución del modelo_ completa, es decir

Emodelo[sisj]=∑v,hp(v,h) sisj=1Z∑v,he−E(v,h)sisj.\mathbb{E}_{\text{modelo}}[s_i s_j] = \sum_{v,h} p(v,h)\,s_i s_j = \frac{1}{Z}\sum_{v,h} e^{-E(v,h)} s_i s_j.

El cálculo exacto de esta suma es en general **intratable** porque implica sumar sobre todas las $2^M$ posibles configuraciones (donde $M$ es el número total de unidades). De hecho, se ha probado que el problema de inferencia y aprendizaje en una BM es NP-hard: hay que realizar “sumas múltiples intractables sobre todas las configuraciones posibles”. En la práctica esto significa que computar exactamente el gradiente requiere evaluar la función de partición $Z=\sum_{v,h}e^{-E(v,h)}$ o las expectativas del modelo, lo cual escala exponencialmente con el número de unidades. Este coste prohibitivo hace que el cálculo exacto del gradiente de log-verosimilitud sea intratable para redes de tamaño moderado.

_Detalle de la demostración._ Insertando la forma $p(v,h)\propto\exp(-E)$ en la log-verosimilitud, al derivar surge la diferencia de dos términos: la media del producto $s_i s_j$ bajo la distribución empírica (datos) y bajo la distribución del modelo. Mientras el primero se estima con los datos observados, el segundo requiere computar

∑v,hsisjexp⁡(−E(v,h))\sum_{v,h} s_i s_j \exp(-E(v,h))

que implica enumerar _todas las configuraciones_. Como subraya Carreira-Perpiñán y Hinton (2005), este cómputo implica “sumas múltiples intractables sobre todas las posibles configuraciones”. Formalmente, calcular el gradiente equivale a resolver un problema NP-hard. En resumen, la parte difícil del gradiente es obtener el valor exacto de la media bajo el modelo (fase negativa), lo que requiere normalizar con $Z$ y manejar $2^M$ términos, por lo que en general es intractable.

## Pregunta 3: Algoritmo de Gibbs para una RBM y convergencia ergódica

Una **RBM (Restricted Boltzmann Machine)** tiene estructura bipartita: una capa visible $v$ y una capa oculta $h$ sin conexiones dentro de cada capa. Para muestrear de la distribución modelo $p(v,h)\propto e^{-E(v,h)}$, el método estándar es el **muestreo de Gibbs alternado** en bloques. El algoritmo es:

1. Partir de algún estado inicial $(v,h)$ (por ejemplo, inicializar $v$ con datos o al azar).
    
2. **Bloque oculto:** muestrear cada $h_j \sim \text{Bernoulli}(\sigma(c_j + \sum_i w_{ij}v_i))$, donde $\sigma(x)=1/(1+e^{-x})$ y $c_j$ es el sesgo oculto. Esto actualiza todo $h$ condicionalmente a $v$.
    
3. **Bloque visible:** muestrear cada $v_i \sim \text{Bernoulli}(\sigma(b_i + \sum_j w_{ij}h_j))$, donde $b_i$ es el sesgo visible. Esto actualiza $v$ dado el nuevo $h$.
    
4. Repetir 2–3 alternando hasta convergencia o hasta realizar $k$ pasos deseados.
    

Debido a la bipartición, las distribuciones condicionales factoran:

p(hj=1∣v)  =  σ(cj+∑iwijvi),p(vi=1∣h)  =  σ(bi+∑jwijhj).p(h_j=1\mid v)\;=\;\sigma(c_j + \sum_i w_{ij}v_i), \qquad p(v_i=1\mid h)\;=\;\sigma(b_i + \sum_j w_{ij}h_j).

Estas fórmulas se derivan directamente de $p(v,h)=\exp(-E)/Z$. El **operador de transición** de un paso completo de Gibbs (v→h→v) define una cadena de Markov en el espacio $(v,h)$. Es fácil mostrar que cumple la propiedad de **detailed balance** respecto de $p(v,h)\propto \exp(-E)$, por construcción del muestreo condicional. Por tanto la distribución modelo es estacionaria para esta cadena. Además, si asumimos condiciones naturales de irreducibilidad y aperiodicidad (por ejemplo, conexiones no degeneradas y posibilidad de autotransiciones), la cadena es **ergódica**. En concreto, debido a que cualquier estado $(v,h)$ puede alcanzarse con probabilidad positiva en un número finito de pasos, y que no hay ciclos periódicos estrictos, la cadena converge al único estado estacionario. En conclusión, el muestreo de Gibbs bloque-a-bloque en una RBM define una cadena ergódica cuya distribución límite es justamente la distribución de Boltzmann $p(v,h)$.

_Prueba esquemática._ El **operador de transición de Gibbs** de la RBM cumple _detailed balance_: para dos estados $(v,h)$ y $(v',h')$ consecutivos, $p(v,h),T((v,h)\to(v',h')) = p(v',h'),T((v',h')\to(v,h))$, garantizando que $p$ es estacionaria. Por otro lado, la cadena es _irreducible_ (cualquier estado alcanza cualquier otro en varios pasos con probabilidad no nula) y puede hacerse _aperiódica_ (p.ej. incluyendo la posibilidad de no cambiar un bit con cierta probabilidad). El teorema fundamental de cadenas de Markov en espacios finitos asegura entonces que la cadena converge a la distribución estacionaria única. En resumen, el Gibbs sampling bloqueante en RBM explora todo el espacio de estados y, bajo condiciones de aperiodicidad, es ergódico con distribución límite $p(v,h) \propto e^{-E(v,h)}$.

## Pregunta 4: Regla de aprendizaje Contrastive Divergence (CD-$k$) y aproximación del gradiente

El **Contrastive Divergence (CD-$k$)** es una aproximación al gradiente de log-verosimilitud basada en truncar el muestreo de Gibbs. Recordemos que el gradiente exacto de la log-verosimilitud para un peso $w_{ij}$ es

∂L∂wij  =  ⟨vihj⟩data  −  ⟨vihj⟩modelo ,\frac{\partial \mathcal{L}}{\partial w_{ij}} \;=\; \langle v_i h_j \rangle_{\text{data}} \;-\; \langle v_i h_j \rangle_{\text{modelo}}\,,

donde $\langle\cdot\rangle_{\text{modelo}}$ es la media según $p(v,h)$ (fase negativa difícil). La idea de CD-$k$ es estimar $\langle v_i h_j \rangle_{\text{modelo}}$ no exactamente, sino usando una cadena de Gibbs de longitud $k$ iniciada en cada ejemplo de datos. Específicamente:

1. Tomar un dato visible inicial $v^{(0)}$ (fase positiva), muestrear $h^{(0)}\sim p(h\mid v^{(0)})$.
    
2. Alternar $k$ pasos de Gibbs: para $t=1,\dots,k$, muestrear $v^{(t)} \sim p(v\mid h^{(t-1)})$ y luego $h^{(t)} \sim p(h\mid v^{(t)})$. Al final se obtiene una muestra $\tilde v = v^{(k)}, \tilde h = h^{(k)}$ tras $k$ pasos.
    
3. Actualizar los pesos como
    

Δwij=ϵ( vi(0)hj(0)  −  v~i h~j),\Delta w_{ij} = \epsilon\Bigl(\,v_i^{(0)} h_j^{(0)} \;-\; \tilde v_i\,\tilde h_j\Bigr),

o en forma de expectativas: $\Delta w_{ij}\propto \langle v_i h_j\rangle_{\text{dato}}-\langle v_i h_j\rangle_{\text{CD-}k}$.

Una derivación alternativa muestra que CD-$k$ corresponde al gradiente de una función objetivo aproximada. Como señalan Carreira-Perpiñán y Hinton (2005), la actualización de CD-$k$ es proporcional a

−∂F(v(0))∂θ  +  ∂F(v~)∂θ,-\frac{\partial F(v^{(0)})}{\partial \theta} \;+\; \frac{\partial F(\tilde v)}{\partial \theta},

donde $F(v)$ es la energía libre (free energy) de $v$. Luego, $\Delta\theta\propto \partial F(v^{(0)})/\partial\theta - \partial F(\tilde v)/\partial\theta$. En palabras, CD-$k$ intenta empujar la energía libre de los datos hacia abajo y la de la muestra generada hacia arriba. Es fácil ver que cuando $k\to\infty$, la cadena de Gibbs converge a la distribución del modelo $p(v)$, por lo que la muestra $\tilde v$ será una verdadera muestra de $p(v)$, y entonces el término $\langle v_i h_j\rangle_{\text{CD-}k}$ tiende al esperado del modelo, recuperando el gradiente exacto. Así, CD-$k$ con $k$ finito produce un gradiente sesgado pero que para $k$ grandes (o bien ajustando muchos pasos) se aproxima al gradiente verdadero.

_Derivación resumida._ Partimos de $\partial \log p(v)/\partial w_{ij}=v_i\mathbb{E}[h_j|v] - \mathbb{E}[v_i h_j]_{\text{modelo}}$. CD propone aproximar $\mathbb{E}[v_i h_j]_{\text{modelo}}$ con $v_i^{(k)} h_j^{(k)}$, la muestra tras $k$ iteraciones de Gibbs empezando en $v^{(0)}=v_{\text{dato}}$. Según , esto equivale a actualizar $\Delta w_{ij}\propto (v_i^{(0)}h_j^{(0)} - v_i^{(k)}h_j^{(k)})$. Cuando $k\to\infty$, la cadena se mezcla ($\tilde v\sim p$) y la actualización coincide con la diferencia de expectativas original; por tanto, el sesgo desaparece en el límite grande de pasos de Gibbs.

## Pregunta 5: Comparación CD-1 vs CD-$k$: sesgo y varianza del estimador

CD-1 y CD-$k$ se diferencian principalmente en cuán buena es la aproximación al gradiente verdadero y en la varianza del estimador. **Sesgo:** CD-1 (un solo paso de Gibbs) es mucho más _sesgado_ que CD-$k$ para $k>1$, porque la cadena de Gibbs no tiene tiempo de alcanzar la distribución modelo. Como vimos, el sesgo del estimador disminuye al aumentar $k$; de hecho, CD-$k$ converge al gradiente real cuando $k\to\infty$. En la práctica, CD-1 puede sesgar notablemente el aprendizaje, pero sorprendentemente suele dar direcciones de descenso razonables incluso con mucho sesgo.

**Varianza:** Una cadena corta como CD-1 usa menos muestreo y por tanto suele tener menor varianza inherente que un método con muchos pasos (o que MCMC exacto). Carreira-Perpiñán y Hinton observan que CD introduce _menos ruido_ de muestreo que estimaciones MCMC largas. En particular, entrenar con CD (incluso CD-1) conduce a estimadores de gradiente con _varianza reducida_ comparado con el caso de utilizar un muestreo exhaustivo del modelo. En resumen, CD-1 tiene **sesgo alto y varianza relativamente baja**, mientras que CD-$k$ con $k$ mayor reduce el sesgo (mejor aproximación al gradiente) a costa de hacer más muestreo. Hinton et al. señalan explícitamente que CD reduce la varianza del estimador del gradiente.

_Evidencia y comparación._ Hinton et al. demuestran que al entrenar con CD se reduce tanto el costo de cómputo como la varianza del gradiente estimado. Sin embargo, el precio es introducir sesgo. Cuanto mayor sea $k$, más cerca se está del gradiente verdadero (sesgo menor), pero también se necesita más pasos de Gibbs y potencialmente aumenta la varianza debido al muestreo. En la práctica, CD-1 resulta muy popular porque ofrece un buen compromiso: aunque sesgado, tiene suficiente estabilidad (baja varianza) para aprendizaje efectivo.

## Pregunta 6: Actualización de pesos en RBM con unidades ocultas gaussianas y momentos

Consideremos una RBM en la que **las unidades ocultas son continuas gaussianas** (con media lineal y varianza $\sigma^2$) y las visibles binaras. El modelo típicamente define:

p(hj∣v)=N(hj∣μj(v),  σj2),p(vi=1∣h)=σ(bi+∑jwijhj).p(h_j \mid v) = \mathcal{N}\bigl(h_j \mid \mu_j(v),\;\sigma_j^2\bigr), \quad p(v_i=1 \mid h) = \sigma\bigl(b_i + \sum_j w_{ij}h_j\bigr).

En este caso, cada unidad oculta $h_j$ dado $v$ sigue una distribución normal con media lineal $\mu_j(v)=b_j + \sum_i w_{ij}v_i$ y varianza fija $\sigma_j^2$. De la forma de esta distribución Gaussian se deduce que los **momentos condicionales** son

E[hj∣v]  =  bj+∑iwijvi,E[hj2∣v]  =  (bj+∑iwijvi)2+σj2.\mathbb{E}[h_j \mid v] \;=\; b_j + \sum_i w_{ij}v_i, \qquad \mathbb{E}[h_j^2 \mid v] \;=\; \bigl(b_j + \sum_i w_{ij}v_i\bigr)^2 + \sigma_j^2.

En particular, con varianza $\sigma_j^2=1$ (caso común), $\mathbb{E}[h_j \mid v]=b_j+\sum_i w_{ij}v_i$ y $\mathrm{Var}(h_j|v)=1$.

La **regla de aprendizaje** (CD) en esta RBM se mantiene en forma similar:

Δwij  =  ϵ(  Edata[vihj]  −  Emodelo[vihj]),\Delta w_{ij} \;=\; \epsilon\Bigl(\;\mathbb{E}_{\text{data}}[v_i h_j] \;-\; \mathbb{E}_{\text{modelo}}[v_i h_j]\Bigr),

pero ahora $h_j$ es continua. Al muestrear Gibbs se usarían estas expectativas condicionales. Sin embargo, como señala Salakhutdinov et al., para $\sigma_j^2=1$ las actualizaciones son equivalentes a las de la RBM estándar.

_Derivación detallada._ Partimos de la energía de la RBM con $h_j$ gaussianos, que conduce a

p(hj=h∣v)∝exp⁡(−(h−(bj+∑iwijvi))22σj2).p(h_j=h\mid v)\propto \exp\Bigl(-\frac{(h - (b_j+\sum_i w_{ij}v_i))^2}{2\sigma_j^2}\Bigr).

Esto es una normal con media $b_j+\sum_i w_{ij}v_i$. Entonces los momentos condicionales se obtienen como los momentos de una normal. Para el entrenamiento por contraste, la actualización general de pesos sigue siendo $\Delta w_{ij}=\epsilon(\langle v_i h_j\rangle_{\text{data}} - \langle v_i h_j\rangle_{\text{model}})$. La fase de datos utiliza $\mathbb{E}[h_j|v_{\text{dato}}]$ en lugar de $h_j$ binario, es decir $\langle v_i h_j\rangle_{\text{data}}=v_i^{(0)}\mathbb{E}[h_j|v^{(0)}]$. De manera similar, en la fase negativa se usaría $\tilde v_i,\mathbb{E}[h_j|\tilde v]$. Con $\sigma_j^2=1$, Salakhutdinov et al. observan que estas actualizaciones coinciden formalmente con las de una RBM con unidades binarias, lo cual simplifica la implementación. En resumen, las unidades ocultas gaussianas tienen un promedio condicional lineal, y los pesos se actualizan con la misma forma de diferencia de momentos, usando $\mathbb{E}[h_j|v]$ en lugar de muestrear $h_j$ binario.

## Pregunta 7: Relación RBM vs Análisis Factorial probabilístico (peso lineal)

El **análisis factorial probabilístico (FA)** es un modelo lineal para datos reales: asume vectores observables $x$ generados como $x=W h + \mu + \varepsilon$, donde $h$ son factores latentes gaussianos estándar ($h\sim\mathcal{N}(0,I)$) y $\varepsilon$ es ruido gaussiano con covarianza diagonal. Este modelo induce $x\sim\mathcal{N}(\mu,W W^\top + \Psi)$.

Se puede demostrar que una RBM con unidades visibles y ocultas gaussianas (y función de energía cuadrática) equivale a este modelo lineal bajo ciertas condiciones. De hecho, Mark y Movellan (2001) muestran que _una máquina de Boltzmann de productos de expertos con activaciones lineales es equivalente a un factor analyzer_. En particular, si consideramos una RBM donde tanto $v$ como $h$ son gaussianos y la energía es

E(v,h)=12∥v−Wh−μ∥2+12∥h∥2+const,E(v,h) = \frac12 \|v - W h - \mu\|^2 + \frac12 \|h\|^2 + \text{const},

la marginal $p(v)$ resultante corresponde a un GA (Gaussian RBM) con covarianza similar a $WW^\top + I$. En la limitación de activaciones lineales (ninguna saturación), el campo libre decae y la BM actúa como un producto de expertos lineales. Marks & Movellan prueban que este caso coincide exactamente con un modelo de análisis factorial.

_Equivalencia formal._ Bajo pesos y sesgos lineales, la distribución conjunta $p(v,h)\propto\exp(-E(v,h))$ se factoriza de modo que $h\mid v$ y $v\mid h$ son gaussianos lineales, igual que en FA. Marginalizando $h$ se obtiene $p(v)$ gaussiana con media lineal en $v$ y covarianza $WW^T+\sigma^2 I$, idéntica a FA. Como resumen, la RBM lineal (peso lineal, unidades gaussianas) _realiza el mismo cómputo que un factor analyzer_. Esto está expuesto por Marks y Movellan: un PoE con funciones de activación lineales es equivalente a un análisis factorial.

## Pregunta 8: Modelo de mezcla de Gaussianas como BM

Un **modelo de mezcla de gaussianas (MoG)** con $K$ componentes define la densidad visible

p(v)  =  ∑c=1Kπc N(v∣μc,Σc),p(v) \;=\; \sum_{c=1}^K \pi_c \,\mathcal{N}(v\mid\mu_c,\Sigma_c),

donde $\pi_c$ son pesos de mezcla, y cada componente es una gaussiana. Se puede interpretar esto como una BM particular incluyendo variables ocultas que indiquen la componente. Por ejemplo, introduzcamos variables ocultas $h_c$ binarias con la restricción “uno-solo-activo” (uno de los $h_c$ vale 1 y los demás 0). Sea la energía definida por

E(v,h)  =  ∑c=1Khc[12(v−μc)TΣc−1(v−μc)+constc]−∑clog⁡πc hc.E(v,h) \;=\; \sum_{c=1}^K h_c\Bigl[\frac12(v-\mu_c)^T\Sigma_c^{-1}(v-\mu_c) + \text{const}_c\Bigr] - \sum_{c} \log \pi_c\,h_c.

Aquí $h$ solo puede tomar $K$ estados (uno-hot). Entonces la marginal sobre $v$ es

p(v)  =  ∑he−E(v,h)/Z  =  ∑c=1Kπc 1∣2πΣc∣exp⁡(−12(v−μc)TΣc−1(v−μc)),p(v) \;=\; \sum_{h} e^{-E(v,h)}/Z \;=\; \sum_{c=1}^K \pi_c \,\frac{1}{\sqrt{|2\pi\Sigma_c|}} \exp\Bigl(-\tfrac12(v-\mu_c)^T\Sigma_c^{-1}(v-\mu_c)\Bigr),

es decir, exactamente la mezcla de gaussianas (con $Z=1$ por construcción de las constantes). En otras palabras, MoG puede verse como una BM donde la capa oculta elige la componente gaussiana con probabilidad $\pi_c$ y luego $v$ es normal alrededor de $\mu_c$.

Carrazza y Krefl (2018) muestran este fenómeno de modo general: la _parte visible_ de ciertas máquinas de Boltzmann (por ejemplo, la Riemann-Theta BM) se comporta como una mezcla gaussiana compleja. En esencia, un MoG es un BM donde los pesos y biases se configuran para que, condicionado en cada estado oculto, la visible sea gaussiana diferente, y la probabilidad marginal del modelo reproduzca la mezcla. Así, cualquier MoG puede interpretarse como una BM con una capa oculta discreta especializada y energia diseñada apropiadamente.

## Pregunta 9: Descentralización del aprendizaje en máquinas de Boltzmann profundas

Una **Deep Boltzmann Machine (DBM)** tiene varias capas ocultas profundas con conexiones sólo entre capas adyacentes (grafos bipartitos en cada par). Entrenar una DBM completa puede hacerse de forma “descentralizada” mediante entrenamiento capa por capa. En particular, Salakhutdinov y Hinton (2009) demostraron que se puede ensamblar una DBM entrenando primero RBMs locales y luego combinándolas. Concretamente, al entrenar dos RBMs modificados en serie (ajustando la magnitud de los pesos) se obtiene una DBM. Al combinar estas dos “módulos” entrenados, las distribuciones condicionales resultantes coinciden exactamente con las de la DBM completa. Extendiendo esto a más capas, todos los módulos intermedios (excepto primeros y últimos) deben tener sus pesos “repartidos” (por ejemplo, multiplicados por 1/2 en cada sentido) para mantener la simetría.

La prueba clave es que la probabilidad condicional de cada capa oculta dado sus vecinas en la DBM compuesta coincide con la definida por las RBMs preentrenadas. Así, el aprendizaje se **descentraliza**: en lugar de optimizar un modelo global complejo, se entrenan localmente bloques RBM (pares de capas) y luego se ensamblan. Este enfoque “en capas” resulta en un buen punto de partida para el refinamiento posterior y permite además que la inferencia aproximada se realice con un pase hacia arriba rápido por las capas preentrenadas.

_Esquema de la demostración._ Salakhutdinov & Hinton (2009) prueban que si preentrenamos cada par de capas como una RBM (ajustando los pesos a la mitad cuando se combinan), las **condiciones de equilibrio** locales coinciden con las de la DBM completa. En otras palabras, las distribuciones $p(h^{(l)}|h^{(l-1)},h^{(l+1)})$ obtenidas al combinar las RBM preentrenadas son exactamente las mismas que las de la DBM original. Esto implica que el gradiente de log-verosimilitud global se puede aproximar ensamblando gradientes locales; cada RBM puede aprender “localmente” sin requerir la actualización simultánea de todas las capas. Por tanto el aprendizaje se distribuye por capas (descentraliza) y cada módulo optimiza sus parámetros basándose en las activaciones de capas adyacentes entrenadas, obteniéndose al final una DBM coherente.

## Pregunta 10: Criterio de evaluación basado en la función de partición y aproximaciones (ej. AIS)

El **criterio de evaluación** de un modelo generativo como una BM suele ser la **verosimilitud** sobre datos de prueba, es decir el logaritmo de la probabilidad asignada a datos nuevos. Esto involucra la función de partición $Z$: la probabilidad marginal de un dato $v$ es

log⁡p(v;θ)=log⁡(∑he−E(v,h;θ))  −  log⁡Z(θ).\log p(v;\theta) = \log\Bigl(\sum_h e^{-E(v,h;\theta)}\Bigr) \;-\; \log Z(\theta).

En la práctica se suele usar el logaritmo de la función partición en la evaluación, por ejemplo para comparar modelos o hacer selección de hiperparámetros.

Como $Z$ es inalcanzable exacto para BMs grandes, se emplean métodos de _aproximación de $Z$_. Un método destacado es el **Annealed Importance Sampling (AIS)**: se construye una serie de distribuciones intermedias entre un modelo simple con partición conocida $Z_0$ y el modelo objetivo con partición $Z_1=Z$. Se usan cadenas de Markov con temperatura gradual para estimar el cociente $Z_1/Z_0$. En palabras, AIS “simula” un camino de baja a alta temperatura acumulando factores de importancia, lo que permite estimar $\log Z$ con precisión. Salakhutdinov y Murray (2008) demostraron que AIS puede estimar eficientemente la partición de un RBM, y luego Salakhutdinov et al. adaptaron AIS a la DBM. En la práctica, se inicia en una distribución base (p.ej. RBM con pesos a cero) y se “enfría” hacia el modelo entrenado, calculando el producto acumulado de factores normalizadores.

Además de AIS, existen otros métodos aproximados: la **pseudoverosimilitud** (maximizar la probabilidad condicional de una variable dado las demás) evita $Z$ completamente, y aproximaciones de cortes (contrastive divergence con mayor $k$) o **estimadores variacionales** ofrecen límites inferiores de la verosimilitud. Pero AIS es uno de los más potentes para evaluar verdaderas probabilidades de modelos basados en energía. En resumen, el criterio es la verosimilitud (dependiente de $Z$) y AIS es una técnica de Monte Carlo avanzada que la aproxima con alta precisión.

_Texto citado:_ Como indican Salakhutdinov et al., se ha usado con éxito AIS para evaluar la partición de RBMs. Un esquema ANNEAL de distribuciones intermediarias $p_k(v)=\exp(-\beta_k E(v))/Z_k$ con $\beta_0=0,\beta_K=1$ permite calcular $\ln Z=\ln Z_K = \ln Z_0 + \sum_k \ln(Z_k/Z_{k-1})$ mediante muestras y factores de importancia. Estos métodos permiten comparar modelos basados en la energía incluso cuando la partición real es inaccesible.

**Fuentes:** Fuentes académicas de libros y artículos especializados sobre máquinas de Boltzmann y aprendizaje profundo, que respaldan las derivaciones y afirmaciones anteriores. Cada afirmación teórica clave se cita según estas referencias.