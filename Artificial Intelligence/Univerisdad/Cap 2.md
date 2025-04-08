### **Resumen Detallado del Capítulo 2: "Intelligent Agents" (Agentes Inteligentes)**

_(Artificial Intelligence: A Modern Approach, 4ta Edición)_

Este capítulo introduce el concepto de **intelligent agents** (agentes inteligentes), explorando cómo perciben su entorno (**environment**), toman decisiones racionales y ejecutan acciones para maximizar su desempeño. Se analiza la relación entre un agente y su entorno, las propiedades de diferentes tipos de entornos y los diversos diseños de agentes.

---

## **2.1 Agents and Environments** (Agentes y Entornos)

Un **agent** (agente) es cualquier entidad que percibe el entorno mediante **sensors** (sensores) y actúa en él mediante **actuators** (actuadores). Un agente puede ser un robot, un software, o incluso un ser humano.

### **Ejemplo: Un coche autónomo (self-driving car)**

- **Sensores:** Cámaras, LIDAR, GPS, acelerómetros.
    
- **Actuadores:** Dirección, frenos, acelerador.
    
- **Proceso:** El coche percibe la carretera, detecta obstáculos y ajusta su velocidad y dirección en consecuencia.
    

El **behavior** (comportamiento) de un agente está determinado por su **percept sequence** (secuencia de percepciones), que es el historial de todas sus entradas sensoriales. Basándose en esta información, el agente elige su próxima acción según su **agent function** (función del agente).

#### **Ejemplo del "Vacuum World" (Mundo del Aspirador)**

Un agente aspiradora puede moverse entre dos ubicaciones (A y B) y percibir si el suelo está sucio o limpio. Su **agent function** podría definir reglas como:

1. Si la ubicación actual está sucia → Aspirar.
    
2. Si la ubicación está limpia → Moverse a la otra ubicación.
    

Este ejemplo ilustra cómo un agente sigue un conjunto de reglas basado en sus percepciones del entorno.

---

## **2.2 Good Behavior: The Concept of Rationality** (Buen Comportamiento: El Concepto de Racionalidad)

Un **rational agent** (agente racional) es aquel que toma decisiones óptimas para maximizar su desempeño según una **performance measure** (medida de desempeño).

### **Factores que influyen en la racionalidad de un agente:**

1. **Performance measure** (Medida de desempeño): Define qué significa tener éxito.
    
    - Un coche autónomo debe minimizar el tiempo de viaje y evitar accidentes.
        
2. **Prior knowledge** (Conocimiento previo): Información que el agente conoce de antemano.
    
    - Un sistema de recomendación usa datos históricos de los usuarios para sugerir películas.
        
3. **Percept sequence** (Secuencia de percepciones): Información recopilada en tiempo real.
    
    - Un robot explorador en Marte ajusta su trayectoria según las imágenes del terreno.
        
4. **Possible actions** (Acciones posibles): Opciones disponibles en cada momento.
    
    - Un asistente de voz puede responder preguntas, ajustar alarmas o pedir más detalles.
        

Un agente racional elige siempre la acción que maximiza su desempeño esperado dado su conocimiento y percepciones.

---

## **2.3 The Nature of Environments** (La Naturaleza de los Entornos)

El entorno de un agente define qué tan fácil o difícil es su tarea. Se clasifica según diferentes dimensiones:

### **1. Fully Observable vs. Partially Observable** (Totalmente Observable vs. Parcialmente Observable)

- **Fully observable:** El agente tiene acceso completo a toda la información relevante del entorno.
    - **Ejemplo:** Un tablero de ajedrez, donde todas las piezas son visibles.
    
- **Partially observable:** Parte de la información no está disponible.
    - **Ejemplo:** Un coche autónomo no puede ver detrás de una curva hasta que gira.


### **2. Single-Agent vs. Multi-Agent** (Un Solo Agente vs. Multiagente)

- **Single-agent:** Solo hay un agente que toma decisiones.
    - **Ejemplo:** Un robot resolviendo un laberinto.
    
- **Multi-agent:** Hay múltiples agentes que pueden colaborar o competir.
    - **Ejemplo:** Un juego de póker donde los jugadores compiten entre sí.


En entornos multiagente, la interacción puede ser **competitive** (competitiva, como en el ajedrez) o **cooperative** (cooperativa, como en un equipo de fútbol).

### **3. Deterministic vs. Stochastic** (Determinístico vs. Estocástico)

- **Deterministic:** Las acciones siempre tienen el mismo resultado esperado.
    - **Ejemplo:** Un programa que ordena números; siempre produce el mismo resultado con los mismos datos.
    
- **Stochastic:** Existe incertidumbre en los resultados.
    - **Ejemplo:** Un asistente de reconocimiento de voz, que puede interpretar una palabra de manera diferente dependiendo del ruido ambiente.


### **4. Static vs. Dynamic** (Estático vs. Dinámico)

- **Static:** El entorno no cambia mientras el agente decide.
    - **Ejemplo:** Resolver un rompecabezas de Sudoku.
    
- **Dynamic:** El entorno puede cambiar mientras el agente actúa.
    - **Ejemplo:** Conducir en el tráfico, donde otros autos y peatones afectan la situación.
    

---

#### **Introducción a la estructura de los _agents_ (agentes)**

Un _agent_ (agente) es una entidad que percibe su entorno y actúa en consecuencia. La efectividad de un _agent_ depende en gran medida de su estructura interna, la cual determina cómo toma decisiones basadas en sus _percepts_ (percepciones). En esta sección del libro se explica cómo se diseñan y estructuran los _agents_ para mejorar su desempeño en diferentes entornos.

---

## **1. Arquitectura y programas de los _agents_**

Cada _agent_ está compuesto por dos elementos fundamentales:

1. **Arquitectura del _agent_** (_agent architecture_):
    - Es la estructura física o computacional sobre la que el _agent_ opera.
    - Puede ser un sistema de hardware, como un robot con sensores y motores, o un programa que se ejecuta en una computadora.
    
2. **Programa del _agent_** (_agent program_):
    - Es la implementación de la función de decisión del _agent_.
    - Toma los _percepts_ del entorno y genera una acción basada en ellos.
    - Se ejecuta sobre la arquitectura del _agent_.


Ejemplo:  
Un automóvil autónomo tiene una arquitectura compuesta por sensores (cámaras, radar, LIDAR), un sistema de procesamiento y actuadores (volante, frenos, acelerador). Su _agent program_ procesa las imágenes de las cámaras, interpreta señales de tránsito y decide cómo conducir.

---

## **2. Tipos de _agents_ basados en su estructura**

Los _agents_ pueden clasificarse en diferentes tipos dependiendo de cómo toman sus decisiones. Se presentan cuatro categorías principales de _agents_:

### **2.1. _Simple reflex agents_ (agentes reflejos simples)**

- Funcionan con la regla **"si ocurre X, entonces haz Y"**.
- No tienen memoria de eventos pasados ni modelan el estado del mundo.
- Se basan en **condiciones de percepción** (_condition-action rules_).

Ejemplo:  
Un termostato es un _simple reflex agent_ porque simplemente enciende la calefacción cuando la temperatura baja de cierto umbral y la apaga cuando la temperatura es lo suficientemente alta.

---

### **2.2. _Model-based reflex agents_ (agentes reflejos basados en modelos)**

- Incorporan un **modelo interno** (_internal model_) del mundo.
- Son capaces de manejar entornos parcialmente observables porque mantienen un estado interno que resume la información pasada.
- Utilizan este estado para tomar mejores decisiones.

Ejemplo:  
Un robot aspirador moderno no solo detecta obstáculos en tiempo real, sino que construye un mapa del entorno para moverse de manera más eficiente.

---

### **2.3. _Goal-based agents_ (agentes basados en objetivos)**

- No solo consideran el estado actual del mundo, sino también los **objetivos** (_goals_) que desean alcanzar.
- Evalúan diferentes acciones en función de si conducen a la consecución del objetivo.
- Requieren técnicas de planificación y búsqueda para determinar el mejor camino hacia la meta.


Ejemplo:  
Un GPS que planifica rutas no solo considera el tráfico actual, sino que también busca la ruta más corta hacia el destino deseado.

---

### **2.4. _Utility-based agents_ (agentes basados en utilidad)**

- Además de trabajar con objetivos, estos _agents_ emplean una **función de utilidad** (_utility function_) que cuantifica la preferencia de ciertos estados sobre otros.
- No solo buscan alcanzar un objetivo, sino que buscan la mejor manera de hacerlo.
- Pueden manejar situaciones donde existen múltiples objetivos con diferentes niveles de importancia.


Ejemplo:  
Un automóvil autónomo no solo busca llegar a su destino (_goal-based agent_), sino que también optimiza la velocidad, el consumo de energía y la seguridad (_utility-based agent_).

---

## **3. _Learning agents_ (agentes de aprendizaje)**

- Son _agents_ que mejoran su desempeño con el tiempo mediante el aprendizaje.
    
- Contienen cuatro elementos principales:
    
    1. **Elementos de aprendizaje** (_learning element_): mejora el rendimiento con la experiencia.
    2. **Elementos de desempeño** (_performance element_): toma decisiones en base a la información disponible.
    3. **Crítica** (_critic_): evalúa el desempeño del _agent_ y proporciona retroalimentación.
    4. **Generador de problemas** (_problem generator_): sugiere acciones nuevas para mejorar el desempeño.


Ejemplo:  
Un chatbot basado en inteligencia artificial aprende de interacciones previas con usuarios y ajusta sus respuestas para mejorar la conversación.

---
