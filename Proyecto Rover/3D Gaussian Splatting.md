- [What is 3D Gaussian Splatting?](https://www.youtube.com/watch?v=Tnij_xHEnXc)
- [3D Gaussian Splatting! - Computerphile](https://www.youtube.com/watch?v=VkIJbpdTujE)
- [Introduction to 3D Gaussian Splatting-Paper Explained & Training on NeRF Studio Gsplats](https://learnopencv.com/3d-gaussian-splatting/)
- [Una NUEVA REVOLUCIÓN en el 3D 👉 GAUSSIAN SPLATTING 👈 - YouTube](https://www.youtube.com/watch?v=_vPwiPuBDnU)

# What is 3D Gaussian Splatting

Es un método para crear una escena 3D compleja usando un video o serie de imágenes. Hace uso de los llamados **Radiance Fields** como **NeRF** con una particularidad. 3D GS es más rápido de entrenar y se pueden lograr un mayor nivel de detalle. 3D GS logra representaciones de escenas en tiempo real de forma increíblemente rápida.

Comenzamos con un conjunto de imágenes (input) desde distintos ángulos de un objeto, o también un video. 

Usando un método matemático llamado **Structure-from-Motion** **[[Notes Paper Surver 3D Gaussian Splatting#Structure-from-Motion (SfM)|SfM]]** las diferencias entre estas imágenes se calculan para formar la nube de puntos 3D. Podemos pensarlo como muchos puntos en el espacio 3D donde cada punto representa un punto de las fotos. Ahora en lugar de intentar crear un modelo detallado con polígonos, cada punto se convierte en un **gaussiano 3D** (un elipsoide) Los gaussianos 3D  tiene parámetros (transparencia, tamaño, color) que les permiten entrar en un proceso de optimización iterativo que les permite afinarlos hasta que coincidan con las fotos originales ajustando sus posiciones 3D, la opacidad del color y **como varian sus detalles desde diferentes direcciones**. El entrenamiento también utiliza un **Adaptative Density Control** (Control de densidad adaptativo), lo que significa que cuando un gaussiano es demasiado transparente, se elimina o cuando un gaussiano es demasiado grande para una parte detallada de la escena, se divide en dos.

Para ver estos gaussianos usamos una técnica llamada **[[Notes Paper Surver 3D Gaussian Splatting#Rasterization|rasterizacion]]** que los proyecta sobre una superficie 2D. Se considera su distancia del espectador para la profundidad y luego para cada píxel se calcula cuánto contribuye cada gaussiano a ese pixel.

![[Pipeline 3D GS.png]]

---

# Paper

##  1 Introduction
El objetivo de la reconstrucción de escenas  3D basada en imágenes es convertir una colección de vistas o videos que capturan una escena en un modelo 3D que puede ser procesado y entendido por computadoras.

Aplicaciones
- Modelado y animación 3D: Creación de modelos digitales para entretenimiento, diseño de productos y visualización arquitectónica
- Navegación robótica: Sistemas que permiten a robots mapear y navegar espacios físicos de forma autónoma
- Preservación histórica: 
- Realidad aumentada/virtual: Integración de elementos virtuales en el mundo real (AR) o creación de entornos completamente virtuales (VR)
- Conducción autónoma: Sistemas que permiten a vehículos percibir y navegar su entorno sin intervención humana.

Los primeros intentos de la reconstrucción de escenas 3D comenzó incluso antes del auge del Depp Learning con campos de luz y métodos básicos de reconstrucción de escenas. NeRF presentó un nuevo enfoque que aprovecha las redes neuronales profundas, esto permite el mapeo directo de coordenadas espaciales a color y densidad. Sin embargo su implementación tenía un costo

- Intensidad computacional: Los métodos basados en NeRF son computacionalmente intensivos, y a menudo requieren tiempos de entrenamiento extensos y recursos sustanciales para el renderizado, especialmente para salidas de alta resolución.
- **Capacidad de edición:** Manipular escenas representadas implícitamente es desafiante, ya que las modificaciones directas a los pesos de la red neuronal no están intuitivamente relacionadas con los cambios en las propiedades geométricas o de apariencia de la escena.
### ¿Por qué es difícil editar en NeRF?

1. **Representación Implícita**
    - **NeRF almacena la escena en los pesos de una red neuronal**
    - **No hay una representación directa de objetos o geometría**
    - **La escena está codificada como una "caja negra" de parámetros**
2. **Ejemplo Práctico** Imagina que quieres:
    - Mover un objeto en la escena
    - Cambiar el color de una pared
    - Eliminar un elemento

    En NeRF, no puedes simplemente:
    - Seleccionar el objeto y moverlo
    - Elegir una superficie y cambiar su color
    - Borrar una parte específica porque todo está entrelazado en los pesos de la red neuronal.

Es en este contexto que aparece el 3D Gaussian splatting (GS), no como una mejora incremental sino como un nuevo enfoque. 3D GS surgió por la necesidad de métodos de renderizado más rápidos y eficientes especialmente para aplicaciones como realidad virtual (VR) y **conducción autónoma** que son altamente sensibles a la latencia. El 3D GS abordó esta necesidad introduciendo una representación de escena explícita y avanzada que modela una escena usando millones de gaussianos 3D aprendibles en el espacio.

3D GS ofrece una flexibilidad que permite controlar los objetos y la dinámica de la escena, un factor crucial en escenarios complejos que involucran geometrías intrincadas y condiciones de iluminación variables.


## 2 BACKGROUND

### 2.1 Problem Formulation

#### 2.1.1 Radiance Field
Un campo de radiancia es una representación de la distribución de luz en un espacio 3D, que captura cómo la luz interactúa con las superficies y materiales en el entorno.
Matemáticamente, un campo de radiancia puede describirse como una función $L : \mathbb{R}^5 \to \mathbb{R}^+$, donde $L(x, y, z, \theta, \phi)$ asigna un punto en el espacio $(x, y, z)$ y una dirección especificada por coordenadas esféricas $(\theta, \phi)$ a un valor de [[Notes Paper Surver 3D Gaussian Splatting#Radiancia|radiancia]] no negativo.

Los campos de radiancia pueden encapsularse mediante representaciones implícitas o explícitas.

#### 2.1.2 Implicit Radiance Field
Un campo de radiancia implícito representa la distribución de la luz en una escena sin definir explícitamente la geometría de la misma. Por ejemplo, en NeRF, se emplea MLP, para mapear un conjunto de coordenadas espaciales $(x, y, z)$ y direcciones de visualización $(\theta, \phi)$ a valores de color y densidad.

La radiancia en cualquier punto no se almacena de forma explícita, sino que se calcula en tiempo real consultando el MLP. Por lo tanto, la función puede escribirse como:

$$L_{\text{implícito}}(x, y, z, \theta, \phi) = \text{MLP}(x, y, z, \theta, \phi). \tag{1}$$

Este formato permite una representación diferenciable y compacta de escenas complejas, aunque a menudo con el costo de una alta carga computacional debido al trazado volumétrico de rayos (_volumetric ray marching_).

#### 2.1.3 Explicit Radiance Field 
En contraste, un campo de radiancia explícito representa directamente la distribución de la luz en una estructura espacial discreta, como una cuadrícula de **[[Notes Paper Surver 3D Gaussian Splatting#Voxel|vóxeles]]** o un conjunto de puntos . Cada elemento en esta estructura almacena la información de radiancia correspondiente a su ubicación respectiva en el espacio. Esto permite un acceso más directo y, a menudo, más rápido a los datos de radiancia, pero a costa de un mayor uso de memoria y, potencialmente, una menor resolución.

Una forma genérica para la representación de un campo de radiancia explícito puede escribirse como:

$$L_{\text{explícito}}(x, y, z, \theta, \phi) = \text{DataStructure}[(x, y, z)] \cdot f(\theta, \phi), \tag{2}$$

donde **DataStructure** podría tener el formato de volúmenes, nubes de puntos, etc. **$f(\theta, \phi)$** es una función que modifica la radiancia en función de la dirección de visualización.


#### 2.1.4 3D Gaussian Splatting: Best-of-Both Worlds
3D GS es un campo de radiancia explícito que incorpora las ventajas de los campos de radiancia implícitos. Usa **gaussianas 3D** aprendibles como una representación flexible y eficiente. Estas gaussianas se optimizan bajo la supervisión de imágenes de múltiples vistas para representar con precisión la escena.

Este pipeline diferenciable basado en gaussianas 3D combina los beneficios de la optimización basada en redes neuronales y el almacenamiento de datos explícitos y estructurados. Este enfoque híbrido busca lograr renderizado en tiempo real de alta calidad, con un tiempo de entrenamiento reducido, especialmente en escenas complejas y salidas de alta resolución.

La representación basada en gaussianas 3D se formula como:

$$L_{\text{3DGS}}(x, y, z, \theta, \phi) = \sum_i G(x, y, z, \mu_i, \Sigma_i) \cdot c_i(\theta, \phi), \tag{3}$$

donde $G$ es la función gaussiana con media $\mu_i$ y covarianza $\Sigma_i$, y $c$ representa el color dependiente de la vista.

### 2.2 Context and Terminology
Varias técnicas y disciplinas de investigación tienen una estrecha relación con 3D GS, que se describirán brevemente en las siguientes secciones para mayor claridad.

#### 2.2.1 Scene Reconstruction and Rendering
En términos generales, la reconstrucción de escenas implica crear un modelo 3D de una escena a partir de una colección de imágenes u otros datos. La renderización es un término más específico que se centra en transformar información legible por computadora (por ejemplo, objetos 3D en la escena) en imágenes basadas en píxeles.

Las técnicas tempranas generaban imágenes realistas basadas en campos de luz [1]-[3]. Los algoritmos de estructura por movimiento [4] y estéreo multi-vista [5] avanzaron aún más este campo al estimar estructuras 3D a partir de secuencias de imágenes. Estos métodos históricos proporcionan una base sólida para técnicas más complejas de reconstrucción y renderización de escenas [34]-[37].

#### 2.2.2 Neural Rendering and Radiance Fields
La renderización neural integra el aprendizaje profundo con técnicas gráficas tradicionales para crear imágenes fotorrealistas. Los primeros intentos utilizaron redes convolucionales para estimar pesos de mezcla [36] o soluciones en espacio de textura [38]. Como se mencionó en la Sec. 2.1.1, el campo de radiancia representa una función que describe la cantidad de luz que viaja en cada dirección a través de cada punto en el espacio. Los NeRFs [8], [9], [12] usan redes neuronales, típicamente MLPs, para modelar los campos de radiancia, permitiendo una renderización de escenas detallada y realista.

#### 2.2.3 Volumetric Representations and Ray-Marching
Las representaciones volumétricas modelan objetos y escenas no solo como superficies sino como volúmenes llenos de materiales o espacio vacío. Esto permite una renderización más precisa de fenómenos como niebla, humo o materiales translúcidos. [[Notes Paper Surver 3D Gaussian Splatting#Ray-Marching|Ray marching]] es una técnica utilizada con representaciones volumétricas para renderizar imágenes trazando la trayectoria de la luz a través de un volumen [11]. NeRF [12] comparte el mismo espíritu del ray-marching volumétrico e introduce muestreo por importancia y codificación posicional para mejorar la calidad de las imágenes sintetizadas. Si bien proporciona resultados de alta calidad, el ray-marching volumétrico es computacionalmente costoso, motivando la búsqueda de métodos más eficientes como 3D GS.

![[ray marching.gif]]

#### Point-based Rendering
La renderización basada en puntos es una técnica para visualizar escenas 3D usando puntos en lugar de polígonos tradicionales. Este método es particularmente efectivo para renderizar datos geométricos complejos, no estructurados o dispersos. Los puntos pueden aumentarse con propiedades adicionales como descriptores neurales aprendibles [39], [40], y renderizarse eficientemente [41], [42], pero este enfoque sufre de problemas como agujeros en la renderización o efectos de aliasing. 3D GS [10] extiende este concepto usando [[Notes Paper Surver 3D Gaussian Splatting#Gaussiano Anisotrópico|Gaussianos anisotrópicos]] para una representación más continua y cohesiva de la escena. 


## 3 3D GAUSSIAN SPLATTING: PRINCIPLES

Consideremos una escena representada por (millones de) gaussianas 3D optimizadas. El objetivo es generar una imagen desde una posición de cámara específica.

Recordemos que NeRFs aborda esta tarea mediante el ray marching volumétrico computacionalmente exigente, muestreando puntos del espacio 3D por píxel. Tal paradigma tiene dificultades con la síntesis de imágenes de alta resolución, fallando en lograr un renderizado en tiempo real, especialmente para plataformas con recursos computacionales limitados.

En contraste, el GS 3D comienza proyectando estas gaussianas 3D en un plano de imagen basado en píxeles, un proceso denominado "splatting" (ver Fig. 3b). Después, el GS 3D ordena estas gaussianas y calcula el valor para cada píxel. Como se muestra en la Fig. 3, el renderizado de NeRFs y GS 3D puede verse como un proceso inverso uno del otro.

![[Pasted image 20250113181039.png]]

Esta figura muestra las diferencias fundamentales entre los enfoques de NeRF y 3D GS para renderizar una escena 3D.
#### NeRF (Parte a)
**Proceso (Backward Mapping)**
1. Se lanza un rayo desde la cámara hacia la escena
2. Se muestrean varios puntos a lo largo del rayo (puntos verdes)
3. Para cada punto:
   - Se alimenta su posición (x, y, z) y dirección (θ, φ) a una red neuronal (MLP)
   - La red predice el color (c) y opacidad (α) para ese punto
4. Finalmente se combinan todos los puntos para obtener el color final del píxel

Desventajas
- Computacionalmente costoso
- Requiere múltiples evaluaciones de la red neuronal
- El muestreo denso de puntos ralentiza el proceso
- Difícil de lograr renderizado en tiempo real

#### 3D Gaussian Splatting (Parte b)
**Proceso (Forward Mapping)**
1. Se tienen Gaussianos 3D preestablecidos (esferas de colores rojo, azul y verde)
2. Cada Gaussiano tiene:
   - Posición en 3D
   - Color
   - Opacidad
   - Matriz de covarianza (define su forma)
3. Se proyectan directamente al espacio de imagen ("Splatting")
4. Se convierten en elipses 2D en la imagen final

Ventajas
- Más eficiente computacionalmente
- No requiere muestreo denso
- Permite renderizado en paralelo
- Puede alcanzar renderizado en tiempo real
- Más adecuado para hardware moderno

Diferencia Clave: Forward vs Backward
- **NeRF (Backward)**: Va desde la cámara hacia la escena, muestreando puntos
- **3D GS (Forward)**: Va desde la escena hacia la cámara, proyectando Gaussianos

Esta diferencia fundamental en el enfoque es lo que hace que 3D GS sea más eficiente y rápido que NeRF, mientras mantiene una calidad visual comparable o superior.

A continuación:
1. Comenzamos con la definición de una gaussiana 3D, que es el elemento mínimo de la representación de escena en GS 3D
2. Describimos cómo estas gaussianas 3D pueden usarse para renderizado diferenciable
3. Introducimos la técnica de aceleración utilizada en GS 3D, que es la clave para el renderizado rápido


### 3.1 Rendering with Learned 3D Gaussians
Una escena está representada por millones de Gaussianos 3D optimizados. El objetivo es generar una imagen desde una pose específica de cámara. A diferencia de NeRF que usa ray marching volumétrico, los Gaussianos 3D (3DGS) proyectan directamente sobre el plano de imagen.

#### Diferencias Principales

| Característica | NeRF | Gaussianos 3D |
|----------------|------|---------------|
| Método | Ray marching volumétrico | Proyección directa ("splatting") |
| Rendimiento | Computacionalmente costoso | Tiempo real posible |
| Escalabilidad | Problemas con alta resolución | Mejor escalabilidad |
| Procesamiento | Muestreo de puntos 3D por píxel | Proyección y ordenamiento de Gaussianos |

#### Propiedades de un Gaussiano 3D

Cada Gaussiano 3D se caracteriza por:

| Propiedad | Descripción | Representación |
|-----------|-------------|----------------|
| Centro (µ) | Posición en espacio 3D | Vector 3D |
| Opacidad (α) | Transparencia | Escalar |
| Matriz de Covarianza (Σ) | Forma 3D | Matriz 3x3 |
| Color (c) | Apariencia dependiente de vista | Armónicos esféricos |

![[Pasted image 20250113171733.png]]

#### Culling de Frustum

Determina qué Gaussianos están fuera del frustum de la cámara para optimizar recursos.

![[frustum culling.gif]]



#### Splatting (Proyección)

La proyección de Gaussianos 3D a 2D se realiza mediante:

$$\Sigma' = J W \Sigma W^T J^T \tag{4}$$

Donde:
- $\Sigma$: Matriz de covarianza 2D proyectada
- $W$: Transformación de vista
- $J$: Jacobiano de la transformación proyectiva

#### Renderización por Píxeles

El color final de un píxel se calcula mediante composición alfa:

$$C = \sum_{n=1}^{|N|} c_n \alpha'_n \prod_{j=1}^{n-1} (1-\alpha'_j) \tag{5}$$

La opacidad final $\alpha'_n$ se calcula como:

$$\alpha'_n = \alpha_n \times \exp(-\frac{1}{2}(x'-\mu'_n)^T {\Sigma'_n}^{-1} (x'-\mu'_n)) \tag{6}$$


![[gaussian 3D.gif]]



Donde:
- $x'$: Coordenadas en espacio proyectado
- $\mu'_n$: Centro proyectado
- $\alpha_n$: Opacidad aprendida
- $c_n$: Color aprendido


#### Tiles (Patches)
- En lugar de procesar píxel por píxel, el sistema divide la imagen en cuadrados de 16×16 píxeles llamados "tiles"
- Si un Gaussiano 3D proyectado cubre varios tiles, se crea una copia para cada tile afectado
- Esto reduce significativamente la carga computacional

#### Renderizado paralelo
- Cada Gaussiano recibe un identificador de tile y un valor de profundidad
- Esta información se codifica en una estructura de bytes (ID en bits superiores, profundidad en bits inferiores)
- El procesamiento es independiente para cada tile, permitiendo paralelización
- Se aprovecha la arquitectura CUDA, tratando los tiles como bloques y los píxeles como threads
- Los píxeles dentro de un mismo tile comparten memoria, mejorando la eficiencia



![[Pasted image 20250113165507.png]]

#### Explicación de la Figura 4

La Fig. 4 muestra el proceso de renderización forward (hacia adelante) del sistema 3D GS, dividido en 4 partes principales (a, b, c, d):

**(a) Proceso de Splatting**
- Se proyectan los Gaussianos 3D (representados como esferas de colores rojo, azul y verde) hacia el espacio de imagen 2D
- Al proyectarse, estos Gaussianos 3D se convierten en elipses 2D en el plano de la imagen

**(b) División en Tiles**
- La imagen se divide en 4 tiles (Tile1, Tile2, Tile3, Tile4)
- Cada tile es una región cuadrada de 16x16 píxeles
- Se puede ver cómo las elipses proyectadas pueden atravesar múltiples tiles

**(c) Proceso de Replicación**
- Para cada Gaussiano que intersecta con un tile, se crea una entrada
- Cada entrada contiene:
  - ID del Tile
  - Valor de profundidad (Depth)
- Un mismo Gaussiano puede aparecer en múltiples tiles

**(d) Renderización Paralela**
- Se muestra cómo se calcula el color final para el Tile1
- Fórmulas matemáticas que indican cómo se combinan los colores (C1, C2, C3, C4)
- El proceso utiliza composición alfa para mezclar los colores


![[Pasted image 20250113165521.png]]

#### Explicación de la Figura 5

La Fig. 5 ilustra el proceso de renderización paralela a nivel de píxel basado en tiles:

##### Componentes Principales
1. **Lista Ordenada de Gaussianos**
   - Todos los Gaussianos del Tile1 se almacenan en memoria compartida
   - Están ordenados por profundidad

2. **Secuencia de Lectura Uniforme**
   - Los píxeles dentro del tile acceden a la misma lista ordenada
   - Esto permite una lectura eficiente de memoria

3. **Acceso Paralelo**
   - Se muestran tres tipos de flechas:
     - Línea sólida: Acceso paralelo
     - Línea punteada con guiones: Superposición
     - Línea punteada: Sin superposición

4. **Proceso de Paso (Pass)**
   - Cada píxel procesa la lista de Gaussianos una sola vez
   - Se aplica la ecuación 5 (Eq. 5) para calcular el color final

#### Propósito de las Figuras

El objetivo principal de estas figuras es explicar:
1. Cómo se transforma la representación 3D a 2D
2. Cómo se organiza la información en tiles para procesamiento eficiente
3. Cómo se implementa el paralelismo para mejorar el rendimiento
4. Cómo se accede y procesa la información de manera eficiente en memoria

Este sistema está diseñado para lograr renderización en tiempo real mientras mantiene la calidad visual, utilizando técnicas de paralelización y gestión eficiente de memoria.


### 3.2 Optimization of 3D Gaussian Splatting
En el núcleo del 3D GS se encuentra un procedimiento de optimización diseñado para construir una amplia colección de Gaussianos 3D que capturan con precisión la esencia de la escena, facilitando así la renderización desde cualquier punto de vista.

La optimización tiene dos aspectos principales:

1. **Propiedades de los Gaussianos**
   - Las propiedades de los Gaussianos 3D deben optimizarse mediante  [[Proyecto Rover/Notes Paper Surver 3D Gaussian Splatting#Renderización diferenciable|renderización diferenciable]]
   - El objetivo es ajustarse a las texturas de una escena dada

2. **Cantidad de Gaussianos**
   - El número óptimo de Gaussianos 3D necesarios para representar determinada escena es desconocido de antemano
   - Una aproximación prometedora es permitir que la red neuronal aprenda automáticamente la densidad de Gaussianos 3D

El texto indica que se explicará:
- En la Sección 3.2.1: Cómo optimizar las propiedades de cada Gaussiano
- En la Sección 3.2.2: Cómo controlar la densidad de los Gaussianos

Estos dos procedimientos están entrelazados dentro del flujo de trabajo de optimización. Por claridad, se omiten las notaciones de la mayoría de los hiperparámetros que se establecen manualmente en el proceso de optimización.


#### 3.2.1 Parameter Optimization

##### Loss Function
Una vez completada la síntesis de la imagen, se puede medir la diferencia entre la imagen renderizada y ground truth (las imágenes reales o de referencia que se usan para entrenar el modelo). Todos los parámetros aprendibles se optimizan mediante descenso de gradiente estocástico usando las funciones de pérdida $\mathcal{l}_1$ y D-SSIM:

$$\mathcal{L} = (1-\lambda)L_1 + \lambda \mathcal{L}_{D-SSIM}  \tag{7}$$

Donde:
- $\lambda \in [0,1]$ es un factor de ponderación
- La función de pérdida de **3D GS** difiere de la de **NeRF**
- NeRF calcula la pérdida a nivel de píxel en lugar de nivel de imagen debido al costoso ray-marching

##### Parameter Update
   - La mayoría de las propiedades de un Gaussiano 3D pueden optimizarse directamente mediante retropropagación
   - Optimizar directamente la matriz de covarianza $\Sigma$ puede resultar en una matriz no semi-definida positiva

**Solución Propuesta**
   - Se optimiza un cuaternión $q$ y un vector 3D $s$
   - $q$ representa rotación
   - $s$ representa escala
   - La matriz de covarianza $\Sigma$ se reconstruye como:
     $$\Sigma = RSS^TR^T$$
   Donde:
   - $R$: Matriz de rotación (derivada de $q$)
   - $S$: Matriz de escalado (derivada de $s$)

3. **Grafo Computacional**
   - Existe un grafo computacional complejo para obtener la opacidad α:
     - $q \text{ y } s \to \Sigma$
     - $\Sigma \to \Sigma'$
     - $\Sigma' \to α$
   - Para evitar el costo de la diferenciación automática, 3D GS deriva los gradientes para $q$ y $s$ para calcularlos directamente durante la optimización


#### 3.2.2 Density Control

##### Initialization
3D GS comienza con el conjunto inicial de puntos dispersos de SfM o inicialización aleatoria. Tenga en cuenta que una buena inicialización es esencial para la convergencia y la calidad de la reconstrucción. Después, se adoptan la densificación y poda de puntos para controlar la densidad de Gaussianos 3D.

##### Point Densification
En la fase de densificación de puntos, 3D GS aumenta adaptativamente la densidad de Gaussianos para capturar mejor los detalles de una escena. Este proceso se centra en áreas con características geométricas faltantes o regiones donde los Gaussianos están demasiado dispersos. El procedimiento de densificación se realizará en intervalos regulares (es decir, después de un cierto número de iteraciones de entrenamiento), centrándose en aquellos Gaussianos con grandes **[[Notes Paper Surver 3D Gaussian Splatting#Gradientes posicionales|gradientes posicionales]]**  en el espacio de vista (es decir, por encima de un umbral específico). Implica ya sea clonar Gaussianos pequeños en [[Notes Paper Surver 3D Gaussian Splatting#Under-reconstructed Areas|áreas sub-reconstruidas]]  o dividir Gaussianos grandes en  [[Notes Paper Surver 3D Gaussian Splatting#Over-reconstructed Regions|regiones sobre-reconstruidas]]  . Para la clonación, se crea una copia del Gaussiano y se mueve hacia el gradiente posicional. Para la división, un Gaussiano grande se reemplaza con dos más pequeños, reduciendo su escala por un factor específico. Este paso busca una distribución y representación óptima de Gaussianos en el espacio 3D, mejorando la calidad general de la reconstrucción.

##### Point Pruning
La etapa de poda de puntos implica la eliminación de Gaussianos superfluos o menos impactantes, lo que puede verse como un proceso de [[Notes Paper Surver 3D Gaussian Splatting#Regularization|regularización]] . Se ejecuta eliminando Gaussianos que son virtualmente transparentes (con $\alpha$ por debajo de un umbral específico) y aquellos que son excesivamente grandes ya sea en el [[Notes Paper Surver 3D Gaussian Splatting#World-space|espacio mundial]] o en el [[Notes Paper Surver 3D Gaussian Splatting#View-space|espacio de vista]] . Además, para prevenir aumentos injustificados en la densidad de Gaussianos cerca de las cámaras de entrada, el valor [[Notes Paper Surver 3D Gaussian Splatting#Alpha cerca de cero|alfa]] de los Gaussianos se establece cerca de cero después de un cierto número de iteraciones. Esto permite un aumento controlado en la densidad de Gaussianos necesarios mientras permite la eliminación de los redundantes. El proceso no solo ayuda a conservar recursos computacionales sino que también asegura que los Gaussianos en el modelo permanezcan precisos y efectivos para la representación de la escena.



## 3D GAUSSIAN SPLATTING: DIRECTIONS

Aunque 3D GS ha alcanzado hitos impresionantes, queda un margen significativo para mejorar, por ejemplo, en requisitos de datos y hardware, algoritmos de renderización y optimización, y aplicaciones en tareas derivadas. En las siguientes secciones, buscamos elaborar sobre versiones extendidas seleccionadas de 3D GS. Estas son:
i) 3D GS eficiente en datos [45]-[55] (Sec. 4.1)
ii) 3D GS eficiente en memoria [56]-[64] (Sec. 4.2)
iii) 3D GS fotorrealista [65]-[80] (Sec. 4.3)
iv) Algoritmos de optimización mejorados [22], [77], [81]-[86] (Sec. 4.4)
v) Gaussianos 3D con más propiedades [87]-[93] (Sec. 4.5)
vi) 3D GS con información estructurada [94]-[96] (Sec. 4.6)

### 4.1 3D GS Eficiente en Datos

Un problema notable de 3D GS es la aparición de [[Notes Paper Surver 3D Gaussian Splatting#Artifacts|artefactos]] en áreas con datos observacionales insuficientes. Este desafío es una limitación prevalente en la renderización de campos de radiancia, donde los datos escasos a menudo conducen a inexactitudes en la reconstrucción. Desde una perspectiva práctica, reconstruir escenas desde puntos de vista limitados es de interés significativo, particularmente por el potencial de mejorar la funcionalidad con entrada mínima.

Se utilizan dos estrategias principales para 3D GS eficiente en datos:

i) Los métodos basados en regularización introducen restricciones adicionales como información de profundidad para mejorar el detalle y la consistencia global [46], [49], [51], [55]. Por ejemplo, DNGaussian [49] introdujo un enfoque regularizado por profundidad para abordar el desafío de la degradación geométrica en vistas de entrada escasas. FSGS [46] diseñó un proceso de Gaussian Unpooling para inicialización y también introdujo regularización de profundidad. MVSplat [51] propuso una representación de volumen de costo para proporcionar pistas geométricas. Desafortunadamente, cuando se trata de un número limitado de vistas, o incluso solo una, la eficacia de las técnicas de regularización tiende a disminuir, lo que lleva a

ii) métodos basados en generalización que se centran especialmente en aprender priors [47], [48], [53]. Una implementación típica es generar Gaussianos 3D que pueden usarse para renderizar directamente sin optimización, usando redes neuronales profundas. Este paradigma típicamente requiere múltiples vistas para el entrenamiento pero puede reconstruir la escena 3D con solo una imagen de entrada. Por ejemplo, PixelSplat [47] propuso muestrear Gaussianos de distribuciones de probabilidad densas. Incorporó un transformador epipolar multi-vista y un truco de reparametrización para evitar mínimos locales y mantener el flujo del gradiente. Splatter Image [48] aplicó GS en un entorno monocular a través de un enfoque basado en aprendizaje, utilizando una red de imagen a imagen 2D que mapea una imagen de entrada a un Gaussiano 3D por píxel. Nótese que este paradigma está principalmente enfocado en la reconstrucción de objetos, y su capacidad de generalización deja mucho espacio para mejorar.



### 4.2 3D GS Eficiente en Memoria
Aunque 3D GS demuestra capacidades notables, su escalabilidad plantea desafíos significativos, particularmente cuando se yuxtapone con métodos basados en NeRF. Este último se beneficia de la simplicidad de almacenar meramente los parámetros de un MLP aprendido. Este problema de escalabilidad se vuelve cada vez más agudo en el contexto de la gestión de escenas a gran escala, donde las demandas computacionales y de memoria aumentan sustancialmente. En consecuencia, existe una necesidad urgente de optimizar el uso de memoria tanto en el entrenamiento como en el almacenamiento del modelo.

Hay dos direcciones principales para reducir el uso de memoria:
i) La primera implica reducir el número de Gaussianos 3D [58], [62], [63], es decir, podar Gaussianos 3D insignificantes. Por ejemplo, Papantonakis et al. [63] propusieron un método de poda consciente de la resolución para podar Gaussianos, reduciendo la cantidad de Gaussianos a la mitad. Lee et al. [58] introdujeron una nueva estrategia de enmascaramiento basada en volumen que reduce eficientemente la cantidad de Gaussianos sin comprometer el rendimiento.

ii) La segunda categoría se centra en comprimir el uso de memoria de las propiedades de los Gaussianos 3D [58], [61], [62]. Por ejemplo, Niedermayr et al. [61] comprimieron el color y los parámetros Gaussianos en libros de códigos compactos, usando medidas de sensibilidad para cuantización efectiva y ajuste fino. HAC [62] predijo la probabilidad de cada atributo cuantizado usando distribuciones Gaussianas y luego diseñó un módulo de cuantización adaptativa. Aunque los métodos actuales logran ratios de compresión de varias a docenas de veces para almacenamiento (después del entrenamiento), sigue habiendo un potencial considerable para reducir el uso de memoria durante la fase de entrenamiento.

### 4.3 3D GS Fotorrealista
El pipeline de renderización actual de 3D GS (Sec. 3.1) es directo e implica varios inconvenientes. Por ejemplo, el algoritmo simple de visibilidad puede llevar a un cambio drástico en el orden de profundidad/mezcla de Gaussianos [10]. El realismo de las imágenes renderizadas, incluyendo aspectos como aliasing, reflejos y [[Notes Paper Surver 3D Gaussian Splatting#Artifacts|artefactos]], puede optimizarse más.

Aquí listamos varios puntos clave para mejorar el realismo:

i) Resoluciones Variables [67], [78]. Debido al paradigma de muestreo discreto (ver cada píxel como un punto único en lugar de un área), 3D GS es susceptible al aliasing cuando trata con resoluciones variables, lo que lleva a bordes borrosos o dentados. Yan et al. [67] argumentaron que esto es principalmente porque los métodos tradicionales de renderización no pueden manejar efectivamente la disparidad entre la frecuencia de muestreo de píxeles y los detalles de alta frecuencia de la escena, llevando a artefactos visuales y problemas de rendimiento. Por lo tanto, introdujeron 3D GS multiescala, donde la escena se representa usando Gaussianos de varios tamaños. Analytic-Splatting [78] adoptó una aproximación analítica de la integral Gaussiana dentro del área del píxel, aprovechando una función logística condicionada para la función de distribución acumulativa para capturar mejor la respuesta de intensidad de los píxeles.

ii) Reflejos [68], [97], [98]. Lograr un renderizado realista de materiales reflectantes es un problema difícil y de larga data en la reconstrucción de escenas 3D. GaussianShader [68] mejoró el renderizado neural para escenas con superficies reflectantes integrando una función de sombreado simplificada con Gaussianos 3D.

iii) Geometría. Una limitación de 3D GS es el descuido de la geometría y estructura subyacente de la escena, particularmente en escenas complejas y bajo condiciones variables de vista e iluminación. Esto genera investigación sobre reconstrucción consciente de la geometría [22], [44], [99]-[102]. Por ejemplo, GeoGaussian[77] se centró en preservar la geometría de regiones sin textura como paredes y muebles, que tienden a degradarse con el tiempo.



### 4.4 Algoritmos de Optimización Mejorados
Los Gaussianos anisotrópicos, aunque beneficiosos para representar geometrías complejas, pueden crear artefactos visuales indeseables. Por ejemplo, esos Gaussianos 3D grandes, especialmente en regiones con apariencia dependiente de la vista, pueden causar artefactos de aparición repentina, donde los elementos visuales aparecen o desaparecen abruptamente, rompiendo la inmersión. Además, incorporar regularización adicional (por ejemplo, geometría [77], [83] y frecuencia [84]) y mejorar el proceso de optimización de 3D GS (Sec. 3.2) puede acelerar la convergencia, suavizar el ruido visual y mejorar la calidad de las imágenes renderizadas.

Destacan tres direcciones principales para mejorar la optimización de 3D GS:

i) Introducir Regularización Adicional [22], [84]. 3D GS a menudo enfrenta desafíos con la sobre-reconstrucción, donde Gaussianos 3D dispersos y grandes causan desenfoque y artefactos debido a una mala representación en regiones de alta varianza. Para abordar esto, FreGS [84] introdujo un método de regularización de frecuencia progresiva, que refina la densificación Gaussiana desde una perspectiva de frecuencia. Otra rama notable es la reconstrucción consciente de la geometría, como se introdujo en la Sec. 4.3. Esta línea de trabajo se centra en particular en cómo preservar la estructura de la escena. Por ejemplo, Scaffold-GS [22] introdujo una cuadrícula dispersa de puntos de anclaje para organizar Gaussianos 3D locales, que se ajustan dinámicamente para atributos como opacidad y color basados en la perspectiva y distancia del espectador.

ii) Mejorar el Procedimiento de Optimización [44], [77]. Al abordar los desafíos de la inicialización densa para superficies sin textura, especialmente en escenas a gran escala, GaussianPro [44] ideó una estrategia avanzada de densificación Gaussiana utilizando los priors de geometrías reconstruidas y técnicas de coincidencia de parches.

iii) Relajar Restricciones en la Optimización [81], [82]. La dependencia de herramientas/algoritmos externos puede introducir errores y limitar el potencial de rendimiento del sistema. Por ejemplo, SfM, comúnmente usado en el proceso de inicialización, es propenso a errores y tiene dificultades con escenas complejas. Yang et al. [81] propusieron COLMAP-Free 3D GS, que introduce continuidad de flujo de video y una representación explícita de nube de puntos para eliminar la necesidad de preprocesamiento SfM.

Aunque impresionantes, los métodos existentes se concentran principalmente en optimizar Gaussianos para reconstruir escenas con precisión desde cero, descuidando un paradigma desafiante pero prometedor que reconstruye escenas de manera few-shot a través de "meta representaciones" establecidas. Ver "aprendizaje de priors físicos desde datos a gran escala" en la Sec. 7 para más información.

### 4.5 Gaussianos 3D con Más Propiedades
A pesar de ser impresionantes, las propiedades del Gaussiano 3D (Sec. 3.1) están diseñadas para usarse solo en la síntesis de nuevas vistas. Al aumentar el Gaussiano 3D con propiedades adicionales, como propiedades lingüísticas [87]-[89], semánticas/de instancia [90]-[92], y espacio-temporales [93], 3D GS demuestra su considerable potencial para revolucionar varios dominios.

Aquí listamos varias aplicaciones interesantes usando Gaussianos 3D con propiedades especialmente diseñadas:

i) Representación de Escenas con Lenguaje Integrado [87]-[89]. Debido a las altas demandas computacionales y de memoria de las actuales representaciones de escenas con lenguaje integrado, Shi et al. [87] propusieron un esquema de cuantización que aumenta el Gaussiano 3D con incrustaciones de lenguaje simplificadas en lugar de las incrustaciones originales de alta dimensionalidad. Este método también mitigó la ambigüedad semántica y mejoró la precisión de consultas de vocabulario abierto al suavizar características semánticas a través de diferentes vistas, guiado por valores de incertidumbre.

ii) Comprensión y Edición de Escenas [90]-[92]. Feature 3DGS [90] integró 3D GS con destilación de campo de características de modelos base 2D. Al aprender un campo de características de menor dimensión y aplicar un decodificador convolucional liviano para sobremuestreo, Feature 3DGS logró velocidades de entrenamiento y renderizado más rápidas mientras permitía una destilación de campo de características de alta calidad, apoyando aplicaciones como segmentación semántica y edición guiada por lenguaje.

iii) Modelado Espacio-temporal [93], [103]. Para capturar la compleja dinámica espacial y temporal de escenas 3D, Yang et al. [93] conceptualizaron el espacio-tiempo como una entidad unificada y aproximan el volumen espacio-temporal de escenas dinámicas usando una colección de Gaussianos 4D. La representación Gaussiana 4D propuesta y el pipeline de renderización correspondiente son capaces de modelar rotaciones arbitrarias en espacio y tiempo y permiten entrenamiento de extremo a extremo.

### 4.6 3D GS con Información Estructurada
En lugar de aumentar el Gaussiano 3D con propiedades adicionales, otra vía prometedora de adaptación a tareas derivadas es introducir información estructurada (por ejemplo, MLPs espaciales y rejillas) adaptada para aplicaciones específicas.

A continuación mostramos varios usos fascinantes de 3D GS con información estructurada especialmente diseñada:

i) Modelado de Expresiones Faciales. Considerando el desafío de crear avatares de cabeza 3D de alta fidelidad en condiciones de vista dispersa, Gaussian Head Avatar [96] introdujo Gaussianos 3D controlables y un campo de deformación basado en MLP. Concretamente, capturó expresiones faciales detalladas y dinámicas optimizando Gaussianos 3D neutrales junto con el campo de deformación, asegurando así tanto la fidelidad del detalle como la precisión de la expresión.

ii) Modelado Espacio-temporal. Yang et al. [94] propusieron reconstruir escenas dinámicas con Gaussianos 3D deformables. Los Gaussianos 3D deformables se aprenden en un espacio canónico, acoplados con un campo de deformación (es decir, un MLP espacial) que modela la dinámica espacio-temporal. El método propuesto también incorporó un mecanismo de entrenamiento de suavizado por recocido para mejorar la suavidad temporal sin costos computacionales adicionales.

iii) Transferencia de Estilo. Saroha et al. [153] propusieron GS in style, un enfoque avanzado para la estilización neural de escenas en tiempo real. Para mantener una apariencia estilizada cohesiva a través de múltiples vistas sin comprometer la velocidad de renderizado, usaron Gaussianos 3D pre-entrenados junto con una rejilla hash multi-resolución y un pequeño MLP para producir vistas estilizadas.

En resumen, incorporar información estructurada puede servir como una parte complementaria para adaptarse a tareas que son incompatibles con la dispersión y el desorden de los Gaussianos 3D.



## 5 APPLICATION AREAS AND TASKS

Basándose en los rápidos avances en 3D GS, ha surgido una amplia gama de aplicaciones innovadoras en múltiples dominios (Fig. 6) como robótica (Sec. 5.1), reconstrucción y representación de escenas dinámicas (Sec. 5.2), contenido generado por IA (Sec. 5.3), conducción autónoma (Sec. 5.4), sistemas médicos (Sec. 5.5), reconstrucción de escenas a gran escala (Sec. 5.6), e incluso otras disciplinas científicas.

### 5.1 Localización y Mapeo Simultáneo (SLAM)

SLAM es un problema computacional central en robótica y sistemas autónomos. Implica el desafío de que un robot/dispositivo entienda su posición en un entorno desconocido mientras mapea simultáneamente el diseño del entorno. SLAM es crítico en varias aplicaciones como vehículos autónomos y navegación robótica.

El núcleo de SLAM es crear un mapa de un entorno desconocido y determinar la ubicación del dispositivo en este mapa en tiempo real. Como resultado, SLAM plantea grandes desafíos para las técnicas de representación de escenas computacionalmente intensivas, pero sirve como un buen banco de pruebas para 3D GS.
```

```
3D GS entra en el dominio SLAM como un enfoque innovador para la representación de escenas. Los sistemas SLAM tradicionales a menudo usan nubes de puntos/surfels o rejillas de vóxeles para representar entornos. En contraste, 3D GS utiliza Gaussianos anisotrópicos para representar mejor los entornos.

Estudios recientes han empleado 3D GS en SLAM, mostrando el potencial y versatilidad de este paradigma:
1. GS-SLAM adoptó una estrategia adaptativa para añadir o eliminar Gaussianos 3D
2. SplaTAM integró un método directo de seguimiento y mapeo en línea
3. Photo-SLAM propuso un mapa Gaussiano híbrido

### 5.4 Conducción Autónoma

La conducción autónoma busca permitir que los vehículos naveguen y operen sin intervención humana. Estos vehículos están equipados con diversos sensores (cámaras, LiDAR, radar) combinados con algoritmos avanzados y modelos de aprendizaje automático.

En la conducción autónoma, 3D GS se puede utilizar para reconstruir una escena mezclando puntos de datos en una representación cohesiva y continua. Esto es particularmente útil para:
- Manejar densidades variables de puntos de datos
- Asegurar una reconstrucción suave y precisa del fondo estático
- Representar objetos dinámicos en una escena

Los marcos principales separaron la escena urbana/callejera en elementos estáticos y dinámicos, donde los elementos dinámicos se modelan usando:
- Grafo Gaussiano dinámico compuesto
- Nubes de puntos combinadas con logits semánticos
- Modelos físicamente restringidos

Profundizando en la representación de escenas consciente de la física y la semántica, se espera que 3D GS pueda servir idealmente como la piedra angular para la percepción del entorno en la conducción autónoma.
