
- NeRF (Neural Radiance Fields 2020)
- Paper de NeRF: NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis.
- Renderización neural: El uso de redes neuronales o técnicas relacionadas para la generación de gráficos por computador.
- Input: Conjunto de imágenes.
- Output: Representación tridimensional para mover la cámara incluso a perspectivas que no están contenidas en el dataset de imágenes original.
- Luma Labs

Distribución Gaussiana 2D, parámetros.
- $\mu_1$

- $\sigma^2_1$

- $\mu_2$

- $\sigma^2_2$

- $\sigma^2_{xy}$

Más un parámetro de color.

Con este objeto ( )

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

Es en este contexto que aparece el 3D Gaussian splatting (GS), no como una mejora incremental sino como un nuevo enfoque. 3D GS surgió por la necesidad de métodos de renderizado más rápidos y eficientes especialmente para aplicaciones como realidad virtual (VR) y **conducción autónoma** que son altamente sensibles a la latencia. El 3D GS abordó esta necesidad introduciendo una representación de escena explícita y avanzada que modela una escena usando millones de gaussianos 3D aprendibles en el espacio.

3D GS ofrece una flexibilidad que permite controlar los objetos y la dinámica de la escena, un factor crucial en escenarios complejos que involucran geometrías intrincadas y condiciones de iluminación variables.


## 2 BACKGROUND

### 2.1 Problem Formulation

#### 2.1.1 Radiance Field
Un campo de radiancia es una representación de la distribución de luz en un espacio 3D, que captura cómo la luz interactúa con las superficies y materiales en el entorno.
Matemáticamente, un campo de radiancia puede describirse como una función $L : \mathbb{R}^5 \to \mathbb{R}^+$, donde $L(x, y, z, \theta, \phi)$ asigna un punto en el espacio $(x, y, z)$ y una dirección especificada por coordenadas esféricas $(\theta, \phi)$ a un valor de radiancia no negativo.

Los campos de radiancia pueden encapsularse mediante representaciones implícitas o explícitas.


#### 2.1.2 Implicit Radiance Field
Un campo de radiancia implícito representa la distribución de la luz en una escena sin definir explícitamente la geometría de la misma. Por ejemplo, en NeRF, se emplea MLP, para mapear un conjunto de coordenadas espaciales $(x, y, z)$ y direcciones de visualización $(\theta, \phi)$ a valores de color y densidad.

La radiancia en cualquier punto no se almacena de forma explícita, sino que se calcula en tiempo real consultando el MLP. Por lo tanto, la función puede escribirse como:

$$L_{\text{implícito}}(x, y, z, \theta, \phi) = \text{MLP}(x, y, z, \theta, \phi). \tag{1}$$

Este formato permite una representación diferenciable y compacta de escenas complejas, aunque a menudo con el costo de una alta carga computacional debido al trazado volumétrico de rayos (_volumetric ray marching_).


#### 2.1.3 Explicit Radiance Field 
En contraste, un campo de radiancia explícito representa directamente la distribución de la luz en una estructura espacial discreta, como una cuadrícula de **vóxeles** o un conjunto de puntos . Cada elemento en esta estructura almacena la información de radiancia correspondiente a su ubicación respectiva en el espacio. Esto permite un acceso más directo y, a menudo, más rápido a los datos de radiancia, pero a costa de un mayor uso de memoria y, potencialmente, una menor resolución.

Una forma genérica para la representación de un campo de radiancia explícito puede escribirse como:

$$L_{\text{explícito}}(x, y, z, \theta, \phi) = \text{DataStructure}[(x, y, z)] \cdot f(\theta, \phi), \tag{2}$$

donde **DataStructure** podría tener el formato de volúmenes, nubes de puntos, etc. **$f(\theta, \phi)$** es una función que modifica la radiancia en función de la dirección de visualización.


#### 2.1.4 3D Gaussian Splatting: Best-of-Both Worlds
3D GS es un campo de radiancia explícito que incorpora las ventajas de los campos de radiancia implícitos. Usa **gaussianas 3D** aprendibles como una representación flexible y eficiente. Estas gaussianas se optimizan bajo la supervisión de imágenes de múltiples vistas para representar con precisión la escena.

Este pipeline diferenciable basado en gaussianas 3D combina los beneficios de la optimización basada en redes neuronales y el almacenamiento de datos explícitos y estructurados. Este enfoque híbrido busca lograr renderizado en tiempo real de alta calidad, con un tiempo de entrenamiento reducido, especialmente en escenas complejas y salidas de alta resolución.

La representación basada en gaussianas 3D se formula como:

$$L_{\text{3DGS}}(x, y, z, \theta, \phi) = \sum_i G(x, y, z, \mu_i, \Sigma_i) \cdot c_i(\theta, \phi), \tag{3}$$

donde $G$ es la función gaussiana con media $\mu_i$ y covarianza $\Sigma_i$, y $c$ representa el color dependiente de la vista.



