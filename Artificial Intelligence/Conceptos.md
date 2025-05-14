# Problema del gradiente de fuga

El **problema del gradiente de fuga** ocurre principalmente en redes neuronales profundas (deep neural networks) y se refiere a la situación en la que los gradientes que se calculan durante el proceso de backpropagation se vuelven extremadamente pequeños en las capas más profundas de la red. Esto provoca que los pesos en estas capas no se actualicen de manera efectiva, dificultando el aprendizaje.

|**Aspecto**|**Descripción**|
|---|---|
|**Origen del problema**|Surge cuando se utilizan funciones de activación como la sigmoide o la tangente hiperbólica, que producen gradientes pequeños al estar en regiones saturadas.|
|**Impacto**|Los gradientes cercanos a cero dificultan que los pesos de las capas profundas cambien durante el entrenamiento.|
|**Resultado final**|Las capas iniciales aprenden lentamente o, en casos extremos, dejan de aprender por completo.|

### **Por qué ocurre en backpropagation**

- Durante la retropropagación, los gradientes se calculan multiplicando las derivadas de las funciones de activación a través de todas las capas.
- Si estas derivadas son pequeñas (como en funciones sigmoides), el gradiente total se reduce exponencialmente conforme aumenta la profundidad de la red.

### **Funciones de activación y gradiente**

|**Función de activación**|**Región Saturada**|**Problema de gradiente**|
|---|---|---|
|Sigmoide|Sí|Sí, gradientes cercanos a cero.|
|Tangente hiperbólica|Sí|Menos grave que la sigmoide, pero sigue presente.|
|ReLU|No|Reduce significativamente este problema.|

### **Soluciones comunes**

1. **Funciones de activación como ReLU**:
    
    - La función ReLU ($f(x) = \text{max}(0, x)$) no se satura para valores positivos, lo que permite gradientes más grandes.
    - Ayuda a mantener un flujo constante de gradientes hacia las capas profundas.
2. **Inicialización de pesos adecuada**:
    
    - Métodos como **He initialization** o **Xavier initialization** ayudan a prevenir la propagación de valores extremadamente pequeños o grandes.
3. **Redes residuales (ResNets)**:
    
    - Introducen conexiones de salto (*skipconnections*) que permiten un flujo más directo de gradientes.
4. **Normalización**:
    
    - Técnicas como **Batch Normalization** estabilizan los gradientes durante el entrenamiento.