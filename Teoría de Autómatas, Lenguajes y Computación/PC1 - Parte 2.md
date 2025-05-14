
# Estructura
Para elaborar un trabajo que resuma la Teoría de la Computación, te sugiero estructurarlo en secciones claras y bien definidas. A continuación, te doy las pautas paso a paso:

### 1. **Introducción**
   Breve explicación de qué es la Teoría de la Computación y por qué es relevante.
   - Define la Teoría de la Computación.
   - Introduce conceptos clave como **algoritmos**, **computabilidad** y **complejidad**.
   - Indica el objetivo del trabajo: resumir los principales conceptos y teorías.

### 2. **Modelos de Computación**
   Esta sección debe explicar los principales modelos de computación que forman la base de la teoría. Los modelos describen cómo las máquinas pueden realizar cálculos.
   
   | Modelo | Descripción | Ejemplo |
   |--------|-------------|---------|
   | Máquina de Turing | Un modelo abstracto que simula el comportamiento de una computadora mediante una cinta infinita que almacena símbolos y una cabeza lectora/escritora. | Máquina de Turing Universal |
   | Autómata Finito | Modelo de máquina que tiene un número finito de estados, puede leer una secuencia de entradas y cambiar entre estos estados. | Autómata de estados para un detector de contraseñas. |
   | Gramáticas Formales | Sistema de reglas que describe cómo formar cadenas válidas en un lenguaje formal. | Gramáticas de Chomsky (regulares, contextuales, etc.) |

### 3. **Teoría de la Computabilidad**
   Explica qué problemas pueden ser resueltos por una máquina de Turing o un algoritmo.
   
   | Concepto | Descripción | Ejemplo |
   |----------|-------------|---------|
   | Decidibilidad | Un problema es decidible si existe un algoritmo que siempre da una respuesta sí o no en un tiempo finito. | Problema del camino más corto en grafos. |
   | Problemas indecidibles | Problemas que no pueden ser resueltos por ninguna máquina de Turing. | Problema de la parada. |
   | Funciones computables | Funciones que pueden ser calculadas por una máquina de Turing. | Suma de dos números. |

### 4. **Teoría de la Complejidad Computacional**
   Aquí se trata de explicar cómo se mide la eficiencia de los algoritmos y cómo se clasifican los problemas según su dificultad.
   
   | Clase | Descripción | Ejemplo |
   |-------|-------------|---------|
   | Clase P | Problemas que pueden ser resueltos en tiempo polinomial por una máquina determinista. | Ordenar una lista. |
   | Clase NP | Problemas que pueden ser verificados en tiempo polinomial por una máquina no determinista. | Problema del viajante. |
   | NP-completo | Los problemas más difíciles dentro de NP, si se encuentra una solución eficiente para uno, se resuelven todos los NP. | Satisfiabilidad booleana (SAT). |
   | NP-hard | Problemas al menos tan difíciles como los problemas NP-completos, pero no necesariamente pertenecen a NP. | Optimización del viajante. |

### 5. **Lenguajes Formales y Autómatas**
   Explica la clasificación de lenguajes y los tipos de autómatas que los reconocen.

   | Lenguaje | Autómata Asociado | Ejemplo |
   |----------|-------------------|---------|
   | Lenguajes Regulares | Autómata Finito | Expresiones regulares, patrones de búsqueda. |
   | Lenguajes de Contexto Libre | Autómata de Pila | Análisis sintáctico en compiladores. |
   | Lenguajes Recursivamente Enumerables | Máquina de Turing | Programación con recursión infinita. |

### 6. **Teoremas Fundamentales**
   Presenta los teoremas clave que definen los límites de la computación.
   
   | Teorema | Descripción | Importancia |
   |---------|-------------|-------------|
   | Teorema de la Parada | No existe un algoritmo general que determine si una máquina de Turing se detendrá en un problema dado. | Definió límites de la computación. |
   | Teorema de Cook-Levin | Demuestra que el problema SAT es NP-completo. | Inicia el estudio de los problemas NP-completos. |
   | Teorema de Rice | Todo conjunto no trivial de propiedades sobre las funciones computables es indecidible. | Generaliza el problema de la parada. |

### 7. **Conclusiones**
   - Un resumen rápido de los conceptos discutidos.
   - Reflexiona sobre los límites y aplicaciones de la Teoría de la Computación en la tecnología actual.

### 8. **Referencias**
   Incluye fuentes confiables como libros de teoría de la computación (por ejemplo, *Introduction to the Theory of Computation* de Michael Sipser).

---

Sigue estas pautas para estructurar tu trabajo y asegúrate de desarrollar cada sección de manera clara y concisa. Puedes agregar diagramas o gráficos cuando sea necesario, especialmente en la parte de autómatas o complejidad para hacerlo más visual.