
# Historia de la Inteligencia Artificial

La Inteligencia Artificial tiene sus raíces en múltiples disciplinas, incluyendo la filosofía, las matemáticas, la neurociencia y la informática.

## Antecedentes

| Fecha | Hito                                        | Descripción                                                                                                                         | Autor/Autores                     |
| ----- | ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| 1901  | Análisis de Componentes Principales **PCA** | Método estadístico fundamental para reducción de dimensionalidad, base para el aprendizaje automático                               | Karl Pearson                      |
| 1943  | Modelo de Neuronas Artificiales             | Modelo lógico de funcionamiento neuronal, base de las redes neuronales artificiales                                                 | Warren McCulloch, Walter Pitts    |
| 1950  | Test de Turing                              | Turing publica *Computing Machinery and Intelligence*. Propone un test para determinar si una máquina puede pensar como un humano.  | Alan Turing                       |
| 1955  | Conferencia de Dartmouth                    | Se acuña el término "inteligencia artificial", inicio formal del campo                                                              | John McCarthy y colaboradores     |
| 1958  | Perceptrón                                  | Primer modelo de red neuronal supervisada para reconocimiento de patrones                                                           | Frank Rosenblatt                  |
| 1960  | Inferencia Bayesiana Universal              | Fundamento matemático para el aprendizaje inductivo y predictivo                                                                    | Ray Solomonoff                    |
| 1965  | ELIZA                                       | Uno de los primeros programas de procesamiento de lenguaje natural simulando conversación humana                                    | Joseph Weizenbaum                 |
| 1965  | Sistema Experto DENDRAL                     | Primer sistema experto para deducir estructuras químicas                                                                            | Edward Feigenbaum                 |
| 1972  | Lenguaje PROLOG                             | Lenguaje lógico de programación, fundamental en IA simbólica                                                                        | Alain Colmerauer, Robert Kowalski |
| 1980  | Sistema experto R1 (XCON)                   | Primer sistema experto comercial exitoso, usado en configuración de equipos                                                         | Digital Equipment Corporation     |
| 1981  | Connection Machine                          | Computadora paralela diseñada para procesamiento masivo en IA                                                                       | Danny Hillis                      |
| 1982  | Proyecto FGCS (Japón)                       | Iniciativa japonesa para desarrollar computadoras inteligentes con paralelismo masivo                                               | MITI (Gobierno Japonés)           |
| 1982  | Self-Organizing Map (SOM)                   | Red neuronal para aprendizaje no supervisado y visualización de datos                                                               | Teuvo Kohonen                     |

### ❄️ Épocas "frías" o inviernos de la IA

- **Primer Invierno de la IA (mediados de los 70 a principios de los 80):**  
    Las expectativas poco realistas, las limitaciones tecnológicas y los recortes en la financiación (como resultado del Informe ALPAC en 1966 y el Informe Lighthill en 1973) llevaron a una desaceleración significativa en la investigación y desarrollo de IA.
- **Segundo Invierno de la IA (finales de los 80 a principios de los 90):**  
    A pesar del auge de los sistemas expertos en los años 80, su mantenimiento era costoso y complejo. El colapso del mercado de máquinas Lisp en 1987 y la creciente frustración con los resultados provocaron otra caída en la financiación e interés por la IA.



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