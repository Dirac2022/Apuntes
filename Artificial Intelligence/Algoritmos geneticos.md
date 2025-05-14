

Los **algoritmos genéticos (GA)** son una clase de métodos de búsqueda y optimización inspirados en la evolución natural y la genética. Su estudio se remonta a la década de 1960 con los primeros trabajos de Fraser, Burnell y Bremermann en simulación evolutiva, pero alcanzaron su formalización moderna con John Holland en 1975 (libro _Adaptation in Natural and Artificial Systems_). Holland estableció los conceptos básicos de los GA —como la representación binaria de soluciones y los operadores genéticos de selección, cruzamiento y mutación—, y demostró teóricamente cómo evolucionan las poblaciones de soluciones. Desde entonces, los GA han sido ampliamente aplicados en optimización, aprendizaje automático y problemas de ingeniería.

## Representación de soluciones (cromosomas)

En un GA cada **solución candidata** se codifica como un **cromosoma** (o individuo), que suele ser un vector finito de **genes**. Formalmente, sea un espacio de búsqueda $S$ (por ejemplo, ${0,1}^L$ para codificación binaria de longitud $L$). Un cromosoma es una cadena $\mathbf{x}=(g_1,g_2,\dots,g_L)\in S$, donde cada $g_i$ (gen) toma un valor en un alfabeto finito (por ejemplo ${0,1}$) o rango definido. Los distintos valores posibles de un gen se llaman _alelos_. La población en la generación $t$ se denota $P^{(t)}={\mathbf{x}_1^{(t)},\dots,\mathbf{x}_N^{(t)}}$, con $N$ individuos. La representación binaria (bits 0/1) es común en GA clásicos, pero también existen codificaciones reales (componentes flotantes) o enteras, dependiendo del problema. En problemas de permutación (como rutas) se usan cromosomas como secuencias permutadas de índices. La elección de la representación debe reflejar la naturaleza del problema; por ejemplo, en optimización continua se puede usar codificación real, mientras que en problemas combinatorios suele usarse codificación binaria o de permutación.

## Función de aptitud (fitness)

La **función de aptitud** $f: S \to \mathbb{R}$ evalúa la calidad de cada cromosoma. Dado un cromosoma $\mathbf{x}\in S$, su aptitud $f(\mathbf{x})$ refleja qué tan buena es la solución (a menudo a maximizar). Por ejemplo, en un problema de maximización se puede definir $f(\mathbf{x})$ igual a la función objetivo. Si se trata de un problema de minimización, se suele convertir en maximización (por ejemplo, $f(\mathbf{x})=-\text{Costo}(\mathbf{x})$). La función de aptitud debe incorporar restricciones y objetivos del problema de forma adecuada. En cada generación se **evalúa** la aptitud de todos los individuos de la población, asignando un escalar a cada $\mathbf{x}_i^{(t)}$. Esta puntuación permite comparar y ordenar las soluciones. Un diseño apropiado de la función de aptitud es crítico, ya que guía la búsqueda hacia las regiones del espacio de soluciones con mejor desempeño.

## Selección

El operador de **selección** elige qué individuos serán padres para la reproducción, favoreciendo los de mayor aptitud. Los métodos comunes incluyen:

- **Selección por ruleta (proporcional a aptitud):** cada individuo $\mathbf{x}_i$ es seleccionado con probabilidad $p_i = f(\mathbf{x}_i)/\sum_j f(\mathbf{x}_j)$. Así, soluciones con mayor aptitud tienen mayor chance de reproducirse. Formalmente, si $f_i=f(\mathbf{x}_i)$, entonces $p_i = \frac{f_i}{\sum_{j=1}^N f_j}\quad (i=1,\dots,N)$. Este método es equivalente a hacer girar una ruleta donde el tamaño de cada porción es proporcional a $f_i$.
    
- **Selección por torneo:** se escogen al azar $k$ individuos de la población (un _torneo_), y se elige el de mejor aptitud entre ellos para ser padre. Este proceso puede repetirse para seleccionar varios padres. El método de torneo no requiere normalizar aptitudes y controla la presión selectiva mediante el tamaño del torneo.
    
- **Selección por ranking:** se ordenan los individuos por aptitud y se asignan probabilidades de selección en función de su posición (rank) en lugar de la aptitud cruda. Por ejemplo, el individuo con el i-ésimo mejor fitness puede recibir probabilidad $\propto (N-i+1)$ o alguna función monotónica. Esto evita que diferencias extremas en aptitud dominen la selección.
    

Otros métodos incluyen selección truncada, por emparejamiento probabilístico, ruleta por descuento, etc. En general, la selección introduce un sesgo hacia soluciones de alta aptitud mientras mantiene diversidad al permitir cierta probabilidad de que soluciones menos aptas también sean seleccionadas.

## Cruce o recombinación

El **cruce (crossover)** combina información genética de dos padres para generar uno o más descendientes. Dados dos padres $\mathbf{p},\mathbf{q}\in S$ (cada uno con $L$ genes), los operadores de cruce comunes son:

- **Cruce de un punto (one-point):** se elige aleatoriamente un punto de corte $k$ ($1\le k<L$). El hijo $\mathbf{c}$ toma los primeros $k$ genes del padre $\mathbf{p}$ y los últimos $L-k$ genes del padre $\mathbf{q}$, es decir, $\mathbf{c} = (p_1,\dots,p_k,q_{k+1},\dots,q_L)$. De manera simétrica se puede producir otro hijo invertido. Esto combina segmentos contiguos de ambos padres.
    
- **Cruce de dos puntos (two-point):** se eligen dos puntos de corte $k<l$. El hijo toma los genes $1$ a $k$ de $\mathbf{p}$, del $k+1$ al $l$ de $\mathbf{q}$, y del $l+1$ al $L$ nuevamente de $\mathbf{p}$, es decir, $\mathbf{c}=(p_1,\dots,p_k,q_{k+1},\dots,q_l,p_{l+1},\dots,p_L)$ (y otro hijo intercambiando roles). Esto permite mezclar dos segmentos de los padres.
    
- **Cruce uniforme (uniform):** para cada posición $i=1,\dots,L$, se decide al azar de cuál padre tomar el gen (por ejemplo con probabilidad $0.5$). Es decir, $c_i = p_i$ con probabilidad 0.5, o $c_i = q_i$ con probabilidad 0.5. Esto genera hijos con mezcla aleatoria de genes, incrementando diversidad genética.
    

Formalmente, el operador de cruce puede verse como una función $C: S\times S \to S^k$ (comúnmente $k=1$ o 2 hijos). Por ejemplo, en cruce de un punto:  
$$C(\mathbf{p},\mathbf{q}) = \mathbf{c},\quad c_i = \begin{cases}p_i & \text{si }1\le i\le k,\\ q_i & \text{si }k<i\le L,\end{cases} $$ 
y opcionalmente otro hijo intercambiando $\mathbf{p}$ y $\mathbf{q}$. Los operadores de cruce se eligen según la estructura del problema; en permutaciones (viajes, asignaciones) se usan operadores especiales (p.ej. Order Crossover) que respetan la validez de la permutación. En codificaciones binarias o reales, los métodos anteriores son frecuentes. El cruce permite explorar combinaciones de rasgos buenos (building blocks) de los padres.

## Mutación

La **mutación** introduce cambios aleatorios en el cromosoma hijo para mantener diversidad. Se define un operador $M:S\to S$ que, aplicado a cada hijo $\mathbf{c}$, altera algunos genes. Los tipos comunes son:

- **Mutación por voltear bit (bit-flip):** en codificación binaria, cada gen $c_i\in{0,1}$ se invierte con una probabilidad pequeña $p_m$ (por ejemplo $p_m=1/L$). Formalmente, $c'_i = 1-c_i$ con probabilidad $p_m$, o $c'_i=c_i$ con probabilidad $1-p_m$. De esta forma se exploran nuevos vectores cercanos en el espacio.
    
- **Mutación uniforme (reset):** en codificaciones discretas, se selecciona con probabilidad $p_m$ cada gen $c_i$ y se le asigna aleatoriamente otro valor del alfabeto.
    
- **Mutación gaussiana (en real-codificado):** en cromosomas reales, se agrega un ruido gaussiano a cada gen con probabilidad $p_m$: $c'_i = c_i + \mathcal{N}(0,\sigma^2)$. Esto ajusta valores continuos de manera pequeña aleatoria.
    

En general, el parámetro de mutación $p_m$ debe ser bajo para no destruir la información buena obtenida, pero suficiente para evitar convergencia prematura. La mutación asegura **ergodicidad** (posibilidad de alcanzar todas las soluciones) y ayuda a escapar de óptimos locales.

## Reemplazo y elitismo

Una vez generados los descendientes, se forma la nueva población. En un esquema **generacional completo**, la población parental $P^{(t)}$ se sustituye íntegramente por la nueva población de hijos $P^{(t+1)}$. Sin embargo, existe la posibilidad de **elitismo**, donde se preservan los mejores individuos: por ejemplo, se copian directamente (sin modificar) los $E$ mejores cromosomas de $P^{(t)}$ hacia $P^{(t+1)}$, asegurando que la calidad de la mejor solución no disminuya de una generación a la siguiente. Formalmente, si ordenamos la población $P^{(t)}$ por aptitud, se hace:  
P(t+1)={Top-E(P(t))}  ∪  {Mejores N−E de los descendientes}.P^{(t+1)} = \{\text{Top-}E(P^{(t)})\} \;\cup\; \{\text{Mejores }N-E \text{ de los descendientes}\}.  
Este proceso híbrido (elitista) garantiza monotonicidad ascendente de la mejor aptitud. Otras estrategias incluyen reemplazo uniforme (reemplazar al azar), o esquemas ``steady-state'' donde solo unos pocos individuos son reemplazados cada vez. El elitismo suele mejorar la convergencia al retener soluciones óptimas previas.

## Criterios de parada

El algoritmo genético itera (evaluar-aplicar operadores) hasta que se cumple un **criterio de parada**. Los criterios más comunes son:

- Se alcanza una **aptitud objetivo**: existe una solución con $f(\mathbf{x})$ mayor o igual a un umbral deseado.
    
- Se alcanza un **número fijo de generaciones** ($t = T_{\max}$).
    
- Se alcanza un **límite de cómputo** (tiempo o número de evaluaciones de fitness).
    
- La **aptitud óptima deja de mejorar** (convergencia); por ejemplo, no hay mejoras significativas en las últimas $k$ generaciones.
    
- Criterio de inspección manual (usuario detiene si la solución es aceptable).
    

Generalmente se combina alguno de los anteriores, p. ej. “máximo 1000 generaciones o hasta alcanzar $f(\mathbf{x})\ge f^*$”.

## Notación Matemática Formal

A continuación resumimos formalmente los conceptos clave:

- **Espacio de búsqueda**: $S$ es el conjunto de todas las soluciones codificadas (por ejemplo $S={0,1}^L$).
    
- **Cromosoma**: $\mathbf{x}=(g_1,\dots,g_L)\in S$, donde $g_i$ es el valor del gen $i$.
    
- **Población**: $P^{(t)}={\mathbf{x}_1^{(t)},\dots,\mathbf{x}_N^{(t)}}$ denota la población en la generación $t$.
    
- **Función de aptitud**: $f: S \to \mathbb{R}$. La aptitud de $\mathbf{x}_i^{(t)}$ se denota $f_i^{(t)} = f(\mathbf{x}_i^{(t)})$. Suponemos maximización de $f$.
    
- **Selección (ruleta)**: la probabilidad de seleccionar $\mathbf{x}_i^{(t)}$ como padre es $p_i = \dfrac{f_i^{(t)}}{\sum_{j=1}^N f_j^{(t)}}$. En selección por torneo, la selección se define mediante un procedimiento estocástico de comparación.
    
- **Cruce (un punto)**: si $\mathbf{p}=(p_1,\dots,p_L)$ y $\mathbf{q}=(q_1,\dots,q_L)$ son padres, y $k$ es el punto de corte, un hijo es $\mathbf{c}$ con: $c_i = p_i$ para $i\le k$, $c_i = q_i$ para $i>k$. Formalmente, $C_{1punto}(\mathbf{p},\mathbf{q};k) = (p_1,\dots,p_k,q_{k+1},\dots,q_L)$.
    
- **Mutación (binaria)**: para cada gen $g_i$ de un individuo, con probabilidad $p_m$ se muta: gi′={1−gicon probabilidad pm,gicon probabilidad 1−pm.g'_i = \begin{cases}1-g_i & \text{con probabilidad }p_m,\\ g_i & \text{con probabilidad }1-p_m.\end{cases} En notación de Bernoulli, $g'_i = g_i \oplus b_i$ donde $b_i \sim \text{Bernoulli}(p_m)$.
    
- **Reemplazo generacional**: $P^{(t+1)}$ está formado por los nuevos hijos (y tal vez individuos elitistas de $P^{(t)}$).
    
- **Criterio de parada**: se detiene cuando $t \ge T_{\max}$ o $\max_i f(\mathbf{x}_i^{(t)}) \ge f^*$, u otra condición de convergencia.
    

## Pseudocódigo general de un Algoritmo Genético

A continuación se presenta un pseudocódigo genérico de un GA. Cada línea incluye comentarios explicativos:

```
Generar poblaci\u00f3n inicial P(0) de N individuos aleatorios  # Paso 1: inicializar con soluciones diversas
Evaluar aptitud f(x) para cada x en P(0)                     # Paso 2: calcular f de cada individuo
t \u00aa 0                                                   # Inicializar contador de generaciones
Mientras NO se cumpla criterio de parada:                    # Bucle principal hasta la condición de fin
    Seleccionar padres de P(t) seg\u00fan aptitud           # Paso 3: elegir individuos mediante ruleta/torneo/etc.
    Aplicar cruce (crossover) a los padres para crear hijos  # Paso 4: combinaci\u00f3n de genes de los padres
    Aplicar mutaci\u00f3n a los hijos                          # Paso 5: introducir variaci\u00f3n aleatoria en los hijos
    Evaluar aptitud f(x) para cada hijo                      # Calcular f de los nuevos individuos
    Formar nueva poblaci\u00f3n P(t+1) con los mejores hijos   # Paso 6: reemplazar (con o sin elitismo)
    t \u00aa t+1                                             # Avanzar a la siguiente generaci\u00f3n
FinMientras
Devolver mejor soluci\u00f3n encontrada                       # Salida: el individuo de mayor aptitud
```

Cada línea del pseudocódigo se corresponde con los pasos descritos arriba. Por ejemplo, la selección escoge padres basándose en la aptitud relativa, el cruce combina cromosomas (p.ej. un punto), la mutación altera genes aleatoriamente, y el reemplazo forma la nueva población quizás aplicando elitismo. El bucle se repite hasta cumplir un criterio de parada (por número de generaciones o aptitud deseada).

## Ejemplo 1: Optimización de una función matemática (maximización)

**Formulación:** Supongamos el problema de maximizar la función unidimensional f(x)=x2f(x) = x^2 en el dominio discreto $x\in{0,1,\dots,31}$. El objetivo es encontrar el $x$ que maximice $f(x)$. Formalmente: max⁡x∈{0,…,31}f(x)=x2.\max_{x\in\{0,\dots,31\}} f(x) = x^2.

**Representación cromosómica:** Cada posible solución $x$ se codifica como un cromosoma binario de longitud 5 (ya que $2^5=32$ cubre $0\le x\le31$). Es decir, un cromosoma $\mathbf{x}=(b_4b_3b_2b_1b_0)_2$, donde $x = b_4 2^4 + b_3 2^3 + \dots + b_0 2^0$. Por ejemplo, el número decimal 13 sería $(0,1,1,0,1)_2$. Esta codificación binaria es directa y simple. Justificación: el dominio es enteros de 0 a 31, que se representa naturalmente con 5 bits.

**Población inicial (Paso 1):** Generamos aleatoriamente una población de 4 cromosomas (por simplicidad). Supongamos que obtenemos:

1. $\mathbf{x}_1 = (1,0,1,1,0)_2 = 22$
    
2. $\mathbf{x}_2 = (0,1,1,0,1)_2 = 13$
    
3. $\mathbf{x}_3 = (1,1,0,0,1)_2 = 25$
    
4. $\mathbf{x}_4 = (0,0,1,1,1)_2 = 7$
    

**Evaluación de aptitud (Paso 2):** Calculamos $f(x) = x^2$ para cada individuo:

- $f(22) = 484$
    
- $f(13) = 169$
    
- $f(25) = 625$
    
- $f(7) = 49$
    

**Selección (Paso 3):** Aplicamos selección tipo ruleta. Primero hallamos la suma de aptitudes: $S = 484+169+625+49 = 1327$. Las probabilidades de cada individuo son:

- $p_1 = 484/1327 \approx 0.365$
    
- $p_2 = 169/1327 \approx 0.127$
    
- $p_3 = 625/1327 \approx 0.471$
    
- $p_4 = 49/1327 \approx 0.037$
    

Generamos dos padres por esta probabilidad (simulamos una ruleta). Por ejemplo, podemos obtener los padres: padre A = $\mathbf{x}_3 = 25$, padre B = $\mathbf{x}_1 = 22$ (la selección es aleatoria pero favorece a 25 y 22 por sus mayores probabilidades).

**Cruce (Paso 4):** Realizamos cruce de un punto con los padres. Supongamos que el punto de corte aleatorio es en la posición 3 (contando desde la izquierda). Entonces:

- Padre A $(25) = (1,1,0,0,1)_2$
    
- Padre B $(22) = (1,0,1,1,0)_2$  
    Dividimos: los primeros 3 bits de A y últimos 2 de B forman el hijo $\mathbf{c}_1$, y viceversa para $\mathbf{c}_2$.
    
- Hijo1: primeros 3 bits de A $(1,1,0)$ + últimos 2 bits de B $(1,0)$ = $(1,1,0,1,0)_2 = 26$.
    
- Hijo2: primeros 3 bits de B $(1,0,1)$ + últimos 2 bits de A $(0,1)$ = $(1,0,1,0,1)_2 = 21$.
    

**Mutación (Paso 5):** Con probabilidad $p_m=0.1$ (por ejemplo) examinamos cada bit de cada hijo para potencial mutación. Supongamos que al revisar los bits aleatoriamente, el hijo1 muta en el bit 2 (de izquierda a derecha) y el hijo2 no muta:

- Hijo1 original $(1,1,0,1,0)$, mutamos el tercer bit cambiándolo a $(1,1,{\color{red}1},1,0) = (11010)_2 = 26$ (en este caso ya era 26, quedó igual tras la mutación del bit que resultó idéntico al original).
    
- Hijo2 permanece $(1,0,1,0,1) = 21$.
    

**Evaluación de aptitud de la descendencia:** Recalculamos $f$ de los nuevos hijos:

- $f(26) = 676$
    
- $f(21) = 441$
    

**Reemplazo (Paso 6):** Formamos la nueva población. Pongamos que aplicamos elitismo con $E=1$: conservamos el mejor individuo original (que era 25 con $f=625$) y los dos mejores hijos. Ordenamos por aptitud: originales $[25 (625), 22 (484), 13 (169), 7 (49)]$; hijos $[26 (676), 21 (441)]$. El mejor global es 26 (nuevo hijo). Con elitismo dejamos 26 y 25, luego elegimos los siguientes mejores para completar 4 individuos. Así, podríamos tener:  
Nueva población: ${26,,25,,22,,21}$ con aptitudes ${676,625,484,441}$.

Tras una generación, la mejor solución hallada es 26 con $f=676$. El GA continuaría iterando de esta manera hasta cumplir el criterio (p.ej., alcanzar $f\ge 961$ correspondiente a $x=31$ o hasta cierto número de generaciones). En este ejemplo sencillo el proceso ilustra cómo la selección y cruza tienden a incrementar progresivamente la aptitud media de la población.

**Pseudocódigo específico (Ejemplo 1):**

```
Definir N=4, longitud cromosoma L=5, f(x)=x^2 
Inicializar poblaci\u00f3n con 4 individuos binarios aleatorios
Calcular aptitud de cada individuo (f(x))
t \u00aa 0
Mientras (t < T_{\max} y mejor aptitud < objetivo):
    Seleccionar por ruleta 2 padres basados en f
    Realizar cruza de 1 punto para crear 2 hijos
    Aplicar mutaci\u00f3n con p_m=0.1 en cada bit de cada hijo
    Calcular aptitud de cada hijo
    Formar nueva poblaci\u00f3n conservando el mejor individuo (elitismo)
    t \u00aa t+1
FinMientras
```

_Comentarios:_ Cada línea sigue la lógica del algoritmo genérico, pero aplicada al caso de maximizar $x^2$. La **población** está en ${0,1}^5$, la **aptitud** es $f(x)=x^2$. La _selección_ usa ruleta según $f(x)$, el _cruce_ es un punto entre dos padres binarios, y la _mutación_ invierte bits aleatoriamente con baja probabilidad. El uso de elitismo garantiza que no se pierde la mejor solución encontrada hasta el momento.

## Ejemplo 2: Problema de la mochila 0-1

**Formulación matemática:** Considérese el problema clásico de la mochila: dadas $n$ objetos, cada uno con peso $w_i$ y valor $v_i$, maximizar el valor total sin exceder la capacidad $W$ de la mochila. Variables $x_i\in{0,1}$ indican si se toma el objeto $i$ o no. Se plantea:  
max⁡∑i=1nvixis.a.∑i=1nwixi≤W,  xi∈{0,1}.\max \sum_{i=1}^n v_i x_i \quad\text{s.a.}\quad \sum_{i=1}^n w_i x_i \le W,\; x_i\in\{0,1\}.  
Aquí la función a maximizar es $f(\mathbf{x})=\sum v_i x_i$ (si $\sum w_i x_i \le W$) y $f(\mathbf{x})=0$ o penalizada en caso contrario.

**Datos de ejemplo:** Tomemos $n=4$ objetos con los siguientes parámetros y capacidad $W=20$:

|Objeto $i$|Peso $w_i$|Valor $v_i$|
|:-:|:-:|:-:|
|1|3|266|
|2|13|442|
|3|10|671|
|4|9|526|

La mejor solución determinística es tomar los objetos 3 y 4 (peso $10+9=19\le20$, valor $671+526=1197$).

**Representación cromosómica:** Usamos un cromosoma binario de longitud 4: cada gen $x_i$ indica si se incluye el objeto $i$. Así, $\mathbf{x}=(x_1,x_2,x_3,x_4)\in{0,1}^4$. Ejemplo: $\mathbf{x}=(0,1,0,1)$ significa tomar objetos 2 y 4. Esta representación es natural para el 0-1 knapsack.

**Población inicial:** Generamos 4 individuos binarios de largo 4 aleatoriamente. Supongamos que la población inicial es:

1. $\mathbf{x}_1=(1,1,0,1)$ (objetos {1,2,4})
    
2. $\mathbf{x}_2=(0,1,1,0)$ (objetos {2,3})
    
3. $\mathbf{x}_3=(1,0,1,1)$ (objetos {1,3,4})
    
4. $\mathbf{x}_4=(0,0,1,0)$ (objeto {3})
    

**Aptitud:** Calculamos el valor total y verificamos el peso. Definimos $f(\mathbf{x})=\sum v_i x_i$ si $\sum w_i x_i \le 20$; si excede, asignamos $f(\mathbf{x})=0$ (o una penalización grande) para descartar soluciones inválidas.

Evaluemos:

- $\mathbf{x}_1$: peso $3+13+9=25>20$ (inválido) $\to f=0$.
    
- $\mathbf{x}_2$: peso $13+10=23>20$ (inválido) $\to f=0$.
    
- $\mathbf{x}_3$: peso $3+10+9=22>20$ (inválido) $\to f=0$.
    
- $\mathbf{x}_4$: peso $10\le20$ y valor $671$ $\to f=671$.
    

En esta población solo $\mathbf{x}_4$ es válida (671), los demás se descartan con $f=0$.

**Selección:** Aplicamos selección por torneo de tamaño 2 (por ejemplo). Se escogen pares al azar:

- Torneo 1 entre $\mathbf{x}_1 (f=0)$ y $\mathbf{x}_4 (f=671)$: gana $\mathbf{x}_4$ (f1er objeto).
    
- Torneo 2 entre $\mathbf{x}_2 (0)$ y $\mathbf{x}_3 (0)$: empatan en 0, digamos que elegimos $\mathbf{x}_2$.
    
- Torneo 3 entre $\mathbf{x}_4 (671)$ y $\mathbf{x}_3 (0)$: gana $\mathbf{x}_4$.
    
- Torneo 4 entre $\mathbf{x}_1 (0)$ y $\mathbf{x}_2 (0)$: todos 0, elegimos $\mathbf{x}_1$.
    

Supongamos seleccionamos para cruzar: Padres A=$\mathbf{x}_4=(0,0,1,0)$ y B=$\mathbf{x}_1=(1,1,0,1)$ (otros torneos podrían repetirse aleatoriamente para más cruces).

**Cruce:** Usamos cruce de un punto. Elijamos punto de corte después del primer gen ($k=1$).

- Padre A = $(0,0,1,0)$, Padre B = $(1,1,0,1)$.
    
- Hijo1: primeros 1 bits de A $(0)$ + últimos 3 bits de B $(1,0,1)$ = $(0,1,0,1)$ = toma {2,4}.
    
- Hijo2: primeros 1 bit de B $(1)$ + últimos 3 bits de A $(0,1,0)$ = $(1,0,1,0)$ = toma {1,3}.
    

**Mutación:** Probabilidad de mutar cada bit $p_m=0.1$. Supongamos que en Hijo1 muta aleatoriamente el bit 4 (de 0 a 1), y en Hijo2 no muta.

- Hijo1 original $(0,1,0,1)$ muta a $(0,1,0,{\color{red}0})=(0,1,0,0)$ (ahora sólo objeto 2).
    
- Hijo2 permanece $(1,0,1,0)$.
    

**Aptitud de hijos:** Calculamos $f$ de los hijos mutados:

- Hijo1 $(0,1,0,0)$: peso $13\le20$, valor $442$, $\to f=442$.
    
- Hijo2 $(1,0,1,0)$: peso $3+10=13\le20$, valor $266+671=937$, $\to f=937$.
    

**Reemplazo:** Incorporamos los hijos en la población (sin elitismo o con elitismo mínimo). Por ejemplo, reemplazamos los 2 primeros padres por estos 2 hijos, manteniendo los otros dos padres. Nueva población (suponiendo reemplazo total generacional):

1. $(0,1,0,0)$ (hijo1, $f=442$)
    
2. $(1,0,1,0)$ (hijo2, $f=937$)
    
3. $\mathbf{x}_3=(1,0,1,1)$ (viejo, $f=0$)
    
4. $\mathbf{x}_4=(0,0,1,0)$ (viejo, $f=671$)
    

Orden por aptitud: $[937,;671,;442,;0]$. El mejor encontrado es $(1,0,1,0)$ con $f=937$. El óptimo teórico es $1197$, así que continuamos GA con nuevas generaciones para intentar encontrar $(0,1,1,1)$ o $(1,0,1,1)$, etc.

**Pseudocódigo específico (Ejemplo 2):**

```
Definir N=4, n=4 objetos, capacidad W=20
Inicializar poblaci\u00f3n con 4 vectores binarios aleatorios
Para cada individuo x en poblaci\u00f3n: 
    Calcular peso=\u2211 w_i x_i y valor=\u2211 v_i x_i
    Si peso \u2264 W entonces f(x)=valor, sino f(x)=0
t \u00aa 0
Mientras (t < T_{\max} y soluci\u00f3n no encontrada):
    Seleccionar pares de padres (p.ej. torneo de 2)
    Aplicar cruce (un punto) para generar hijos
    Aplicar mutaci\u00f3n con prob. baja en cada gen de los hijos
    Para cada hijo: calcular peso y valor, asignar f como arriba
    Formar nueva poblaci\u00f3n (reemplazo generacional o elitista)
    t \u00aa t+1
FinMientras
```

_Comentarios:_ Cada cromosoma es un vector binario $(x_1,\dots,x_4)$ que codifica la selección de objetos. La función de aptitud $f(x)$ es la suma de valores si no se excede la capacidad, o 0 en caso contrario. En cada generación se seleccionan padres (torneo), se cruzan para formar nuevos vectores, y se muta aleatoriamente cada gen. Finalmente se evalúan los hijos según la función de aptitud especificada. El pseudocódigo mantiene la estructura del algoritmo genérico adaptada al problema de mochila: la **aptitud** considera una restricción de capacidad, la **selección** y **operadores genéticos** son iguales que en el caso general.

Cada uno de estos ejemplos ilustra el uso paso a paso de los operadores de un GA: se define primero la codificación (cromosoma), luego se calcula la aptitud de la población inicial, y se aplican iterativamente selección, cruce, mutación y reemplazo, actualizando la población hasta hallar una solución óptima o cumplir criterios de parada. El procedimiento comentado garantiza rigor académico y claridad en cada etapa del algoritmo.

**Fuentes:** Este contenido se basa en conceptos estándar de algoritmos genéticos, estructurados con notación matemática formal y ejemplos detallados para ilustrar cada componente del GA.