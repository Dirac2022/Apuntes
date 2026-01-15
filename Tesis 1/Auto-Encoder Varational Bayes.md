
**Resumen**  
¿Cómo podemos realizar inferencia y aprendizaje eficientes en modelos probabilísticos dirigidos, en presencia de variables latentes continuas con distribuciones posteriores intratables y grandes conjuntos de datos? Introducimos un algoritmo de inferencia variacional estocástica y aprendizaje que escala a grandes conjuntos de datos y, bajo algunas condiciones leves de diferenciabilidad, incluso funciona en el caso intratable. Nuestras contribuciones son dos. Primero, mostramos que una reparametrización de la cota inferior variacional produce un estimador de la cota inferior que puede optimizarse de manera directa usando métodos estándar de gradiente estocástico. Segundo, mostramos que para conjuntos de datos i.i.d. con variables latentes continuas por punto de dato, la inferencia posterior puede hacerse especialmente eficiente ajustando un modelo de inferencia aproximado (también llamado modelo de reconocimiento) a la distribución posterior intratable usando el estimador de cota inferior propuesto. Las ventajas teóricas se reflejan en los resultados experimentales.

Perfecto 🙌. Vamos con la **traducción fiel** y luego con la **explicación breve y directa**.

---


**1 Introducción**  
¿Cómo podemos realizar inferencia aproximada y aprendizaje eficientes con modelos probabilísticos dirigidos cuyas variables latentes continuas y/o parámetros tienen distribuciones posteriores intratables? El enfoque bayesiano variacional (VB) implica la optimización de una aproximación a la distribución posterior intratable. Desafortunadamente, el enfoque común de _mean-field_ requiere soluciones analíticas de expectativas con respecto a la distribución posterior aproximada, las cuales también son intratables en el caso general.

Mostramos cómo una reparametrización de la cota inferior variacional produce un estimador simple, diferenciable y no sesgado de la cota inferior; este estimador SGVB (_Stochastic Gradient Variational Bayes_) puede usarse para inferencia aproximada eficiente de la distribución posterior en casi cualquier modelo con variables latentes continuas y/o parámetros, y puede optimizarse fácilmente usando técnicas estándar de ascenso por gradiente estocástico.

Para el caso de un conjunto de datos i.i.d. y variables latentes continuas por cada punto de dato, proponemos el algoritmo **Auto-Encoding VB (AEVB)**. En el algoritmo AEVB hacemos que la inferencia y el aprendizaje sean especialmente eficientes al usar el estimador SGVB para optimizar un modelo de reconocimiento que nos permite realizar una inferencia posterior aproximada muy eficiente utilizando un simple muestreo ancestral, lo que a su vez nos permite aprender eficientemente los parámetros del modelo, sin necesidad de esquemas de inferencia iterativos costosos (como MCMC) por cada punto de dato.

El modelo de inferencia posterior aproximado aprendido también puede usarse para una gran cantidad de tareas tales como reconocimiento, eliminación de ruido (_denoising_), representación y propósitos de visualización. Cuando se usa una red neuronal para el modelo de reconocimiento, llegamos al **autoencoder variacional (VAE)**.

---

### 🤔 Explicación breve y directa

1. **Problema**:
    
    - Queremos hacer inferencia en modelos probabilísticos con variables ocultas continuas.
        
    - El problema: la **posterior es intratable** (no se puede calcular exactamente).
        
2. **Solución clásica (mean-field VB)**:
    
    - Aproximamos la posterior con una distribución simple.
        
    - Pero aún así, muchas veces requiere cálculos analíticos imposibles.
        
3. **Lo que proponen**:
    
    - Usar una **reparametrización** para obtener un estimador que:
        
        - Sea **no sesgado** (no distorsiona la expectativa).
            
        - Sea **diferenciable** (podemos usar gradientes).
            
        - Funcione con gradiente estocástico, igual que entrenar redes neuronales.
            
4. **AEVB**:
    
    - Combina SGVB + un **modelo de reconocimiento (encoder)** para aproximar la posterior.
        
    - Ya no necesitas usar métodos lentos como MCMC para cada dato.
        
    - Si el modelo de reconocimiento es una red neuronal → tienes el **VAE**.
        

---

👉 Ejemplo directo:  
Antes, para cada imagen en MNIST tenías que correr un proceso de inferencia largo (como MCMC).  
Con **AEVB**, basta pasar la imagen por una red (el encoder), obtener una distribución para zz, y entrenar con gradiente estocástico → mucho más rápido y escalable.

---

¿Quieres que en la siguiente parte te traduzca y explique la **sección 2: Background**?