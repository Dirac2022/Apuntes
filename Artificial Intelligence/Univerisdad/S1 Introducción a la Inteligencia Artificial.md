
# Historia de la Inteligencia Artificial

La Inteligencia Artificial tiene sus raíces en múltiples disciplinas, incluyendo la filosofía, las matemáticas, la neurociencia y la informática.

## Antecedentes

- 1901, PCA (K. Pearson) inicio IA.
- 1933, Se desarrolla PCA (F. Rosemblatt).
- En 1943, Warren McCulloch y Walter Pits propusieron un modelo de neuronas artificiales inspirado en la función del cerebro humano.
- Alan Turing, en 1950, publicó *Computing Machinery and Intelligence*, donde abordó cuestiones fundamentales sobre la posibilidad de que las máquinas piensen.
- En 1955, John McCarthy organizó la Conferencia de Dartmouth, donde se acuño el término "inteligencia artificial"  y se establecieron los objetivos del campo.
- 1958: Diseño el **Perceptrón**, primera red neuronal de aprendizaje.
- fer
- wef
- wefw
- wef
- 
- wef
- we
- 1982 SOM (T. Kohonen)
- 1987 El 1er invierno de IA
## Primeras demostraciones
Durante los años 50 y 60, surgieron los primeros sistemas que demostraron habilidades inteligentes:

- **Logic Theorist (1956)**: desarrollado por Alen Newell y Herbert Simon, resolvía problemas matemáticos de lógica simbólica
- **Machine Learning**: Arthur Samuel creó un programa de damas capaz de aprender estrategias de juego.

## Crisis y renacimiento

En los años 70, la IA enfrentó problemas debido a expectativas poco realistas y limitaciones computacionales. Sin embargo, en los 80, con la llegada de redes neuronales más avanzadas y sistemas expertos, la IA experimentó un renacimiento.

Hoy en día, la IA se basa en aprendizaje profundo y modelos probabilísticos, permitiendo aplicaciones avanzadas en visión por computadora, procesamiento del lenguaje natural y robótica.


# Definiciones de Inteligencia Artificial


Perspectivas para definir la IA

1. **Humanidad vs Racionalidad**:
	- Actuar o pensar como humano: Enfoque centrado en emular la cognición o comportamiento humano (ejemplo: redes neuronales que imitan el cerebro).
	- Actuar o pensar racionalmente: Enfoque en la toma de decisiones óptimas basadas en lógica o probabilidad (ejemplo: algoritmos de búsqueda en juegos como el ajedrez).

2. **Pensamiento vs. Comportamiento**:
	- Cognición interna: Modelar procesos mentales (ejemplo: sistemas expertos que replican el razonamiento de un médico).
	- Acción externa: Lograr resultados sin necesariamente entender cómo (ejemplo: un robot que navega un laberinto sin "pensar").

Existen múltiples definiciones de IA, dependiendo del enfoque que se adopte​. Podemos clasificarlas en cuatro categorías principales:

1. **Actuar humanamente:** IA que imita el comportamiento humano.
2. **Pensar humanamente:** Modelos que buscan replicar la cognición humana.
3. **Pensar racionalmente:** Uso de la lógica y el razonamiento.
4. **Actuar racionalmente:** Sistemas que toman decisiones óptimas.

Cada enfoque tiene aplicaciones prácticas diferentes. Por ejemplo, la IA en juegos como el ajedrez sigue una estrategia racional, mientras que los chatbots intentan actuar humanamente.


# El Test de Turing
Alan Turing propuso en 1950 una prueba para determinar si una máquina podía exhibir un comportamiento inteligente similar al humano​.

En este test:

- Un humano se comunica con un interlocutor sin saber si es una persona o una máquina.
- Si la máquina engaña al evaluador haciéndole creer que es humana, se considera que ha pasado el test.

>[!tip]  Definición
Sea $H$ un humano, $M$ una máquina e $I$ el interrogador, donde $I$ no sabe quién es quién. La prueba se define así
> 1. $I$ interactúa con $H$ y $M$ a través de un canal de comunicación restringido (como texto)
> 2. $I$ puede hacer preguntas ilimitadas en lenguaje natural
> 3. Si, después de cierto tiempo, $I$ no puede distinguir entre $H$ y $M$ con una precisión mayor que el azar, se dice que $M$ ha pasado el test.


Este enfoque ha sido influyente, aunque criticado. Por ejemplo, una máquina podría engañar sin ser realmente "inteligente". En la práctica, sistemas como _ChatGPT_ pueden imitar el lenguaje humano sin comprenderlo realmente.

**Variantes del Test de Turing**
- **Test de Turing Total:** además del lenguaje, la máquina debe interactuar físicamente con el mundo.
- **Pruebas basadas en tareas específicas:** en lugar de evaluar conversaciones generales, se usan tests en áreas como visión artificial o razonamiento lógico.

>[!note] Clase
> > Si una máquina puede actuar como humano, entonces podemos decir que es inteligente
>Para pasar el Test de Turing debe tener la siguientes características
>- Reconocimiento del lenguaje
>- Razonamiento
>- Aprendizaje
>- Representación del conocimiento
> 
> **Test de Turing total**
> - Visión artificial
> - Robótica
>
> De acuerdo a Turing una máquina será inteligente si actúa y piensa como humano


# La Sala China
John Searle propuso en 1980 el experimento mental de la *Sala China* como una crítica al Test de Turing y a la IA simbólica.

En este experimento
- Un individuo sin conocimiento de chino sigue un conjunto de reglas para manipular símbolos.
- Desde fuera, parece que comprende chino pero en realidad solo sigue instrucciones.


> [!tip] Definición
> Consideremos un sistema $S$ compuesto por:
> 1. **Un humano $P$**: no conoce chino, pero sigue instrucciones.
> 2. **Un conjunto de reglas $R$**: instrucciones detalladas para manipular símbolos chinos.
> 3. **Un conjunto de símbolos $\Sigma$**: caracteres en chino.
> 4. **Un conjunto de respuestas $O$**: secuencias de caracteres en chino generadas por $P$.
> 
> El sistema opera así:
> - $P$ recibe una secuencia de símbolos chinos de entrada $\Sigma_{in}.$
> - Usa $R$ para buscar la respuesta adecuada $\Sigma_{out}.$
> - Entrega $\Sigma_{out}$ como respuesta sin entender su significado.


Searle argumenta que un programa de IA que manipula símbolos no necesariamente entiende su significado. Esta crítica llevó a la distinción entre:

1. **IA débil**: simula inteligencia sin comprender
2. **IA fuerte**: tendría conciencia y comprensión real.

A pesar de las críticas, modelos modernos de IA han logrado superar varias pruebas prácticas, aunque aún no se ha demostrado que posean comprensión real.
- **Sistemas basados en reglas**: Como los primeros sistemas expertos, realizan operaciones simbólicas sin comprensión.
- **Aprendizaje profundo**: Redes neuronales procesan patrones estadísticos, pero ¿construyen significado? El debate sigue abierto.