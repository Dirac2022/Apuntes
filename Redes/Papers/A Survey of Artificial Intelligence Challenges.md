
# Resumen:
En los últimos años, la inteligencia artificial ha tenido un tremendo impacto en todos los campos, y se han proporcionado varias definiciones de sus diferentes tipos. En la literatura, la mayoría de los artículos se centran en las capacidades extraordinarias de la inteligencia artificial. Recientemente, se han reportado algunos desafíos, como la seguridad, la seguridad, la equidad, la robustez y el consumo de energía, durante el desarrollo de sistemas inteligentes. A medida que aumenta el uso de sistemas inteligentes, aumenta el número de nuevos desafíos. Obviamente, durante la evolución de la inteligencia artificial estrecha a la superinteligencia artificial, el punto de vista sobre los desafíos como la seguridad cambiará. Además, el reciente desarrollo de la inteligencia a nivel humano no puede ocurrir adecuadamente sin considerar todos los desafíos en el diseño de sistemas inteligentes. Dada la situación mencionada, ningún estudio en la literatura resume los desafíos en el diseño de inteligencia artificial. En este documento, se presenta una revisión de los desafíos. Luego, se responden algunas preguntas de investigación importantes sobre la dinámica futura de los desafíos y sus relaciones.

Palabras clave: inteligencia artificial; superinteligencia artificial; inteligencia artificial general; inteligencia artificial estrecha; inteligencia a nivel humano; desafíos

# 1. Introducción
La inteligencia artificial (IA) ha sido ampliamente utilizada en los últimos años. En la literatura, numerosos artículos, como [1,2], se centran únicamente en las capacidades extraordinarias de la IA. Pocos documentos, como los reportados en [3–7], se centran en los desafíos de la IA. Durante el análisis de los desafíos de la IA, se han reportado numerosos problemas en la literatura, algunos de los cuales son la seguridad [8], la seguridad [9], la equidad [10], el consumo de energía [11] y la ética [12], por mencionar algunos. El uso generalizado de la IA conduce a la aparición de nuevos desafíos. Este problema se vuelve más complicado cuando las definiciones de los desafíos se modifican basadas en nuevas dimensiones explicadas en el siguiente párrafo.
Desde un punto de vista histórico, la evolución de los sistemas basados en IA comienza con la inteligencia artificial estrecha (ANI), luego continúa con la inteligencia artificial general (AGI) y finalmente alcanza la superinteligencia artificial (ASI), que superará las capacidades humanas en todas las dimensiones [13,14]. Todos los términos mencionados se explicarán en el resto de este documento.
Definir los límites entre las diferentes definiciones de IA y los nuevos conceptos no es una tarea fácil. Además, nos enfrentamos a otras definiciones en esta área, como la inteligencia a nivel humano (HLI), que define un agente que es equivalente a un agente humano en términos de capacidades de pensamiento y actuación. El problema principal es que no hay un estudio exhaustivo en la literatura que discuta los desafíos de la IA que aborden algunas preguntas de investigación sobre la evolución de los desafíos, y también sus relaciones considerando diferentes clases de IA.
**En este documento, se discuten los desafíos de la IA con un enfoque particular en HLI.**
Reunimos 28 desafíos de la literatura, lo que hace que este documento sea único debido a la alta cobertura de desafíos. Para cada desafío, se discute la definición y sus cambios considerando algunas dimensiones en ANI, AGI, ASI e HLI. Después de resumir los desafíos, se responden algunas preguntas de investigación sobre el desarrollo de la IA considerando desafíos para dar una mejor comprensión del desarrollo futuro de la IA. Hasta donde sabemos, no hay un estudio exhaustivo sobre desafíos que se centre en la relación entre los desafíos y su evolución considerando diferentes clases de IA como HLI en la literatura.
El resto del documento está organizado de la siguiente manera. La Sección 2 está dedicada a los preliminares. En la Sección 2, se explican las diferentes clases de IA y los términos relacionados. La Sección 3 se centra en los desafíos. La Sección 4 está dedicada a una discusión detallada sobre los desafíos basada en algunas preguntas de investigación. La última sección está dedicada a las conclusiones.

# 2. Preliminares
Dado que este documento se centra en los desafíos de la IA considerando diferentes términos como ANI, AGI, ASI e HLI, esta sección está dedicada a la definición de los términos mencionados y sus relaciones. Esta sección comienza con una clasificación de la IA para establecer la posición de los estudios existentes sobre IA, y luego se enfoca en HLI debido a su prioridad. Según [15], los sistemas inteligentes se clasifican en tres clases, como se explica a continuación (Figura 1):
- **ANI**: Este tipo de inteligencia se refiere a sistemas inteligentes que realizan tareas específicas. Por ejemplo, un agente con capacidades como reconocimiento facial y juegos. Estos agentes están programados para realizar tareas y no pueden detectar ni formular tareas desconocidas de manera auto organizada. No esperamos ver autoconciencia en estos agentes.
- **AGI**: El concepto de este tipo de inteligencia no se refiere a algo único en la mente de todos los principales científicos de IA. La mayoría de los investigadores utilizan AGI para aquellos agentes cuya inteligencia es equivalente a la de los agentes humanos. AGI puede ser equivalente a HLI.
- **ASI**: En [16], Bostrom introdujo tres tipos de superinteligencia: ASI de velocidad, ASI colectiva y ASI de calidad. **ASI de velocidad se refiere a un agente más rápido que un humano**, **ASI colectiva se refiere a capacidades de toma de decisiones similares a un grupo de humanos**, y **ASI de calidad se refiere a un agente que puede realizar trabajos que los humanos no pueden**.

![[Pasted image 20240505221015.png]]
Figure 1. Venn diagram for definitions of artificial intelligence (AI).

Recientemente, se han realizado algunos cambios en la clasificación anterior. En [17,18], los autores argumentan que HLI es diferente de AGI porque los humanos pueden poner algunas suposiciones y limitaciones en los cálculos de la máquina. Estas suposiciones y limitaciones provienen de la naturaleza humana que heredan las máquinas. Por lo tanto, es posible que AGI no resuelva una amplia gama de problemas que los humanos no pueden resolver. En otras palabras, los humanos establecen algunos límites superiores implícitos en las máquinas y disminuyen las capacidades de generalización. Por otro lado, los autores de algunos documentos, como [18], argumentan que no hay diferencia entre AGI y ASI cuando las definiciones de AGI no están limitadas a HLI. Según [16,18], si las capacidades de los agentes basados en AGI están más allá de la inteligencia humana y no hay una definición exacta de las capacidades de ASI, no hay necesidad de diferenciar AGI de ASI. En consecuencia, en [19], Searle dividió la IA en dos clases: IA débil e IA fuerte. Dado que los desafíos relacionados con HLI serán vitales en el futuro cercano, el resto de esta parte está dedicado a HLI.

HLI se desarrolla en base al conocimiento sobre los humanos, como se ilustra en la Figura 2. Esta figura se divide en: (1) inteligencia humana, (2) ciencias relacionadas con el desarrollo de HLI y (3) desafíos. La parte de inteligencia humana divide el dominio de nuestro conocimiento en Conocido (por ejemplo, la contabilidad es una capacidad conocida de los humanos), Semi-Conocido (por ejemplo, la computación mental es una capacidad semi-conocida de los humanos) y finalmente Desconocido (por ejemplo, los objetivos de la creación humana son un concepto desconocido para los humanos). Se organizaron muchas ciencias basadas en la observación de la inteligencia humana, incluidas las matemáticas y la filosofía. Según [20], varios desafíos se han planteado durante el desarrollo de estas ciencias en el corazón de los sistemas basados en IA. Por lo tanto, la tercera parte de la Figura 2 resume los desafíos de la IA durante el desarrollo de HLI. Cabe destacar que establecer conexiones entre desafíos y sus ciencias relacionadas se basa en artículos informados en la literatura. El número de ciencias relacionadas puede aumentar a medida que el conocimiento de los humanos sobre la IA aumenta.

![[Pasted image 20240505221253.png]]

# 3. Analizando Desafíos 

1. Identificación y Formulación del Problema
2. Consumo de Energía
3. Problemas de Datos
4. Robustez y Fiabilidad
5. Engaño y Decepción
6. Seguridad
7. Privacidad
8. Equidad
9. IA Explicable
10. Responsabilidad
11. Controlabilidad
12. Predictibilidad
13. Aprendizaje Continuo
14. Almacenamiento (Memoria)
15. Semántica y Comunicación
16. Moralidad y Ética
17. Racionalidad
18. Mente
19. Responsabilidad
20. Transparencia
21. Reproducibilidad
22. Evolución
23. Beneficioso
24. Equilibrio entre Exploración y Explotación
25. Verificabilidad
26. Seguridad
27. Complejidad
28. Confiabilidad

# 5. Conclusiones
En este documento, se analizaron los desafíos de la IA con un enfoque particular en HLI. Cabe destacar que las popularidades de los desafíos no eran similares entre sí. En otras palabras, algunos de los desafíos, como la seguridad y la equidad, son más populares que otros desafíos, como la energía y la complejidad. Por lo tanto, se proporcionó una breve descripción para cada desafío para comprender la naturaleza del mismo. Además, se estudiaron las conexiones y combinaciones entre los desafíos, así como sus evoluciones. Dejamos algunos desafíos bien conocidos, como la maldición de la dimensionalidad, debido a su popularidad en el dominio de la IA. Es obvio que durante la evolución desde ANI hasta ASI, todos los desafíos pueden adquirir nuevas dimensiones a medida que descubrimos más información sobre nuestro entorno durante la interacción con sistemas inteligentes. Intentamos abordar este problema en la sección de discusión. Algunos desafíos, como el monopolio de las corporaciones durante la era de la IA, así como la pérdida generalizada de empleos, no estaban dentro del alcance de este documento porque el enfoque de este documento es principalmente en ciencias de la computación. Estos desafíos pueden considerarse en trabajos futuros.
