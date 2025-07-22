
## ¿Qué es la “estimación de profundidad” y por qué importa?

1. **Definición general**  
    La **estimación de profundidad** (depth estimation) es la tarea de calcular la distancia (profundidad) de cada punto de una escena tridimensional a una cámara o sensor, basándose únicamente (o mayoritariamente) en información visual (imágenes o secuencias de vídeo). El resultado típico es un **mapa de profundidad** $D : \Omega \subset \mathbb{R}^2 \to \mathbb{R}^+$, donde:
    
    $$D(x,y) = z$$
    
    significa que en la coordenada de imagen $(x,y)$ la distancia al plano de la cámara es $z$ (en unidades métricas, metros, centímetros, etc.).
    
2. **Aplicaciones principales**
    
    - **Realidad aumentada (AR) y realidad virtual (VR)**: para superponer objetos 3D coherentemente con el entorno real, es imprescindible saber qué partes de la imagen están “más cerca” o “más lejos” de la cámara.
        
    - **Robótica y navegación autónoma**: un robot móvil o un dron debe conocer la geometría tridimensional del entorno para decidir cómo moverse y evitar colisiones.
        
    - **Simultaneous Localization and Mapping (SLAM)**: muchos métodos de SLAM (mapeo y localización simultáneos) requieren estimar profundidad o reconstruir parcialmente la escena.
        
    - **Fotografía computacional**: aplicaciones como el modo retrato de un smartphone (desenfoque selectivo del fondo, bokeh simulado) se basan en un mapa de profundidad para separar sujeto/primer plano y fondo.
        
    - **Reconstrucción 3D**: generar nubes de puntos o mallas 3D a partir de fotografías para tener modelos tridimensionales de edificios, objetos, patrimonio cultural, etc.
        
    - **Análisis de escenas** en visión por computadora: segmentación semántica 3D, detección de objetos en 3D, estimación de poses, etc.
        
3. **¿Por qué “mapas de profundidad” en lugar de “mapas de disparidad” o “nubes de puntos”?**
    
    - Un **mapa de disparidad** (disparity map) suele obtenerse en configuraciones estereoscópicas: la disparidad es inversamente proporcional a la profundidad, y se define como
        
        $$d(x,y) = \frac{B \, f}{Z(x,y)} \quad\Longleftrightarrow\quad Z(x,y) = \frac{B \, f}{d(x,y)},$$
        
        donde $B$ es la distancia (baseline) entre cámaras, ff la distancia focal y $Z(x,y)$ la profundidad real.
        
    - Sin embargo, en muchos proyectos de Inteligencia Artificial y Visión por Computador modernos se prefiere directamente **predecir la profundidad**  $Z(x,y)$ como un valor métrico o relativo, generando un mapa de profundidad. Esto a menudo simplifica la integración con otras partes del sistema (3D reconstructions, navegación, etc.).
        

---

## Aproximaciones para generar mapas de profundidad

Existen varios paradigmas para la estimación de profundidad. A continuación describo los enfoques más comunes, organizados en dos grandes categorías: **clásicos (basados en geometría)** y **aprendizaje automático (machine learning / deep learning)**.

---

### 1. Métodos clásicos basados en estereovisión y técnicas multivista

1. **Estéreo binocular**
    
    - **Principio**: Tomo dos imágenes de la misma escena desde dos cámaras separadas (baseline BB). Identifico correspondencias (feature matching) entre píxeles de la cámara izquierda y la cámara derecha. La disparidad d(x,y) se calcula como la diferencia en coordenada horizontal entre los dos píxeles coincidentes.
        
    - **Cálculo de la profundidad**:
        $$Z(x,y) \;=\; \frac{B \, f}{d(x,y)} \quad\text{o bien}\quad D(x,y) = \frac{1}{d(x,y)} \quad (\text{depth \textit{relative}}).$$
    - **Ventajas**: Puede ser muy preciso si las cámaras están bien calibradas y las correspondencias tienen poco ruido.
        
    - **Desventajas**:
        
        - Requiere un rig estereoscópico físicamente calibrado.
            
        - Dificultad en zonas homógenas (superficies sin textura): “matcheo” de píxeles ambiguo.
            
        - Problemas con oclusiones (cuando un punto visible en la cámara izquierda no es visible en la derecha).
            
    - **Algoritmos representativos**:
        
        - BM (Block Matching)
            
        - SGBM (Semi-Global Block Matching)
            
        - ELAS (Efficient Large-scale Stereo Matching)
            
        - GC (Graph Cuts)
            
        - BM con refinamiento de subpíxel (por ejemplo, interpolación de disparidad entre bordes).
            
2. **Estructura a partir de movimiento (Structure from Motion, SfM)**
    
    - **Principio**: Tomo múltiples imágenes de una escena (desde distintas posiciones o en secuencia de vídeo) con una sola cámara monocular.
        
    - **Pasos básicos**:
        
        1. Detectar y emparejar “features” (SIFT, SURF, ORB, etc.) entre pares de imágenes.
            
        2. Estimar la **posición y orientación** ($R,\,t$) de la cámara en cada vista (requisito de resolver el problema de reconstrucción).
            
        3. Triangular puntos 3D mediante intersección de rayos (método de haz mínimo) usando correspondencias y parámetros intrínsecos de la cámara $(f,\,c_x,\,c_y,\,k_1,\,k_2,\,\ldots)$.
            
        4. Refinamiento conjunto (bundle adjustment) para optimizar el error reproyección:
            $$\min_{\{X_j, R_i, t_i\}} \sum_{i,j} \bigl\|\,\pi\bigl(R_i,X_j + t_i\bigr) - x_{ij}\bigr\|^2,$$
            
            donde $X_j$ es punto 3D, $\pi(\cdot)$ la proyección, $x_{ij}$ la coordenada observada en imagen $i$.
            
    - **Salida**:
        
        - Una nube de puntos 3D (estructura tridimensional).
            
        - Ocasionalmente, se puede interpolar una superficie o un “depth map” si se desea una representación por píxeles.
            
    - **Herramientas clásicas**:
        
        - Bundler, COLMAP, OpenMVG, OpenMVS.
            
    - **Ventajas / Desventajas**:
        
        - Muy preciso en escenas con buena textura y múltiples vistas.
            
        - Mayor carga computacional y necesita buena cobertura de vistas.
            
        - Difícil en escenas poco texturizadas o con movimientos rápidos.
            
3. **Time-of-Flight (ToF) y sensores activos**
    
    - **Principio**: No es estrictamente “visión pasiva”; se envía luz infrarroja modulada al sujeto y se mide el tiempo que tarda en regresar o la fase de la señal.
        
    - **Ejemplos de hardware**: Kinect (primera generación), Intel RealSense, cámaras Myriad IR.
        
    - **Salida**: Un mapa de profundidad “directo” sin tener que hacer correspondencia estereoscópica.
        
    - **Limitaciones**: Alcance limitado, sensibilidad a la luz ambiental, ruido en superficies reflectantes u oscuras.
        

---

### 2. Métodos basados en Deep Learning para estimar mapas de profundidad

Los enfoques basados en aprendizaje profundo han revolucionado la estimación de profundidad, en especial cuando solo se dispone de una **imagen monocular** (monocular depth estimation). A continuación se exponen los enfoques más relevantes:

#### 2.1. Estimación de profundidad supervisada (Monocular, con datos etiquetados)

1. **Concepto básico**
    
    - Si dispongo de un dataset $\mathcal{D} = \{(I_i,\,D_i)\}_{i=1}^N$ donde $I_i$ es una imagen RGB y $D_i$ el correspondiente mapa de profundidad “ground truth” (usualmente obtenido con LiDAR, dispositivo ToF, o rig estéreo de alta calidad), puedo entrenar una red neuronal (por ejemplo, un encoder–decoder) que aprenda la función
        $$\widehat{D} = f_\theta(I),\qquad f_\theta\colon \mathbb{R}^{H\times W\times 3} \;\longrightarrow\; \mathbb{R}^{H\times W},$$
        
        intentando minimizar un error medio entre $\widehat{D}$ y $D$, por ejemplo:
        $$\mathcal{L}(\theta) \;=\; \frac{1}{N} \sum_{i=1}^N \Bigl\|\,f_\theta(I_i) \;-\; D_i\,\Bigr\|_1 \quad\text{o bien}\quad \Bigl\|\,f_\theta(I_i)-D_i\,\Bigr\|_2^2.$$
2. **Arquitecturas comunes**
    
    - **Encoder–decoder con skip-connections** (inspirado en U-Net)
        
        - El encoder extrae características de la imagen (puede basarse en backbones estándar como ResNet, DenseNet, EfficientNet, etc.).
            
        - El decoder va re-muestreando (“up-sampling”) las características para finalmente producir una predicción densa (un mapa de la misma resolución que la imagen original, o ligeramente comprimido).
            
        - Se agregan “skip connections” entre capas simétricas de encoder y decoder para preservar detalles espaciales (bordes, texturas).
            
    - **Redes de “multi-escala”**: incorporan ramas que operan a diferentes resoluciones, de modo que la red capte tanto contexto global (¿en qué zona de la escena estoy?) como detalles locales (¿qué contorno de objeto hay?).
        
    - **Predicción de “planos” o “superficies”**: algunas arquitecturas (por ejemplo, PlaneNet, PlaneRecover) representan la escena como un conjunto de planos y predicen parámetros de planos; luego reensamblan un mapa de profundidad en base a la combinación de varios planos aplicados a distintas regiones de la imagen.
        
3. **Función de pérdida y métricas**
    
    - Las pérdidas más usadas son:
        
        - **L1 Loss (mae)**:
            
            $$\mathcal{L}_1 = \frac{1}{HW} \sum_{x,y} \left|\,\widehat{D}(x,y) - D(x,y)\right|.$$
        - **L2 Loss (mse)**:
            $$\mathcal{L}_2 = \frac{1}{HW} \sum_{x,y} \bigl(\widehat{D}(x,y) - D(x,y)\bigr)^2.$$
	        
		- **Scale-invariant Loss** (propuesto en Eigen et al. 2014):
            $$\large{
            \mathcal{L}_{\text{si}} = \frac{1}{n} \sum_i d_i^2 \;-\; \frac{\lambda}{n^2} \Bigl(\sum_i d_i\Bigr)^2, \quad 
            } \normalsize{\text{donde } d_i = \log \widehat{D}_i - \log D_i}$$
            
            Aquí se penaliza la diferencia de escala logarítmico, de modo que errores absolutos en zonas profundas no pesen tanto como en zonas cercanas.
            
        - **Gradient Loss / Smoothness Loss**: promueve que el mapa de profundidad sea suave donde la imagen no tiene cambios bruscos, pero permita discontinuidades (bordes) en los contornos de objetos.
            
            $$\large{\mathcal{L}_{\text{smooth}} = \sum_{x,y} \bigl|\partial_x \widehat{D}(x,y)\bigr| e^{-\alpha|\partial_x I(x,y)|} + \bigl|\partial_y \widehat{D}(x,y)\bigr| e^{-\alpha|\partial_y I(x,y)|}} $$
            
            Se pesa la suavidad de $D$ con el gradiente de la imagen $I$: si la imagen tiene un borde fuerte ($|\partial I|$ alto), entonces se permite un salto en profundidad ahí.
            
    - **Métricas de evaluación**
        
        - **Abs Rel** (Absolute Relative Error):
            $$\text{AbsRel} = \frac{1}{N} \sum_{i=1}^N \frac{|D_i - \widehat{D}_i|}{D_i}.$$
        - **Sq Rel** (Squared Relative Error):
            $$\text{SqRel} = \frac{1}{N} \sum_i \frac{(D_i - \widehat{D}_i)^2}{D_i}.$$
        - **RMSE (Root Mean Squared Error)**:
            $$\mathrm{RMSE} = \sqrt{ \frac{1}{N} \sum_i (D_i - \widehat{D}_i)^2 }.$$
        - **RMSE log**:
            $$\mathrm{RMSE\, log} = \large{\sqrt{ \frac{1}{N} \sum_i \bigl(\log D_i - \log \widehat{D}_i \bigr)^2 }}$$
        - **$\large{\delta < 1.25^n}$** (Threshold Accuracy): porcentaje de píxeles tales que
            $$\max\left(\frac{\widehat{D}_i}{D_i}, \frac{D_i}{\widehat{D}_i}\right) < 1.25^n, \quad n = 1,2,3$$
            
            Mide la fracción de píxeles cuya predicción está dentro de un factor $1.25$, $1.25^2$, $1.25^3$ de la profundidad real.
            
4. **Ejemplos de redes y papers influyentes**
    
    - **Eigen et al. (2014, 2015)** – “Depth map prediction from a single image using a multi-scale deep network”. Uno de los primeros trabajos en mostrar que un encoder–decoder entrenado de manera supervisada puede predecir mapas de profundidad monocular con buena calidad.
        
    - **Laina et al. (2016)** – “Deeper Depth Prediction with Fully Convolutional Residual Networks”. Utiliza ResNet como encoder e introduce una “BerHu loss” (combinación de $L_1$ y $L_2$ adaptativo) para mejorar el entrenamiento.
        
    - **DORN (2018)** – “Deep Ordinal Regression Network for Monocular Depth Estimation”. Trata la predicción de la profundidad como un problema de regresión ordinal, discretizando la escala de distancias en bins y usando una pérdida ordinal.
        
    - **MegaDepth (2018)** – “MegaDepth: Learning Single-View Depth Prediction from Internet Photos”. Usan SfM para auto-generar mapas de profundidad y entrenar una red en un dataset gigantesco obtenido de fotos de Internet.
        
    - **MiDaS (2020, 2021)** – “Mixed Datasets for Training Monocular Depth Estimation Networks”. Preentrenan una red en varios datasets (KITTI, NYU Depth, TUM, etc.) y luego refinan para obtener predicciones más robustas en escenas “del mundo real”.
        
5. **Ventajas y limitaciones de los métodos supervisados**
    
    - **Pros**:
        - Pueden alcanzar alta precisión si se dispone de suficiente dato “ground truth” de buena calidad.
            
        - Capturan texturas, contextos y características semánticas que ayudan a inferir profundidad en zonas homogéneas (por ejemplo, un muro blanco sin textura).
            
    - **Contras**:
        - Requieren datasets de parejas (imagen, mapa de profundidad) que suelen ser costosos de recolectar (sensores LiDAR, rigs estéreo calibrados, etc.).
            
        - Problemas de **generalización**: un modelo entrenado en un dataset específico (por ejemplo, escenas urbanas de día) puede no funcionar correctamente en otro dominio (interiores, de noche, entornos rurales).
            
        - Dificultad para capturar rangos de profundidad muy grandes (p. e., de centímetros a decenas de metros) sin entrenamiento especializado.
            

---

#### 2.2. Estimación de profundidad mediante auto-supervisión o auto-alineamiento (self-supervised)

Para paliar la necesidad de mapas de profundidad “ground truth”, surgieron métodos que se apoyan en **estéreo no calibrado** o en **secuencias monoculares**, formulando el problema como un **puzzle de reconstrucción**.

1. **Monocular – Video-Based (SfM + Depth Consistency)**
    
    - **Idea clave**: Si tengo una secuencia de vídeo $\{I_t\}$ capturada con una cámara en movimiento, puedo entrenar una red $f_\theta$ que, dada la imagen $I_t$, prediga un mapa de profundidad $\widehat{D}_t$. En paralelo, entreno otra red (“PoseNet”) que prediga la transformación (rotación $R_{t\to t'}$ y traslación $t_{t\to t'}$) de la cámara entre el fotograma $t$ y $t'$.
        
    - **Reproyección**: Con $\widehat{D}_t$ y la estimación de $R_{t\to t'}$,$\,t_{t\to t'}$, puedo “reconstruir” el fotograma $I_{t'}$ proyectando cada píxel de $I_t$ al fotograma $t'$. Denotemos la transformación proyectiva como    $$\large{p_{t\to t'}(x,y) = K\,\bigl[R_{t\to t'}\,(D_t(x,y)\,K^{-1}[x,y,1]^T) + t_{t\to t'}\bigr],}$$
        donde KK es la matriz intrínseca de la cámara.
        
    - **Loss de reconstrucción**: La red se entrena minimizando la diferencia entre el fotograma real $I_{t'}$ y el reconstruido $\widehat{I}_{t'}$. Por ejemplo:
        $$\large{\mathcal{L}_{\text{recon}} = \sum_{x,y} \bigl\|\;I_{t'}\bigl(u,v\bigr) \;-\; I_{t}(x,y)\bigr\|},$$
        donde $(u,v) = p_{t\to t'}(x,y)$ es la posición proyectada en $I_{t'}$.
        
    - **Smoothness y consistencia**: Se agregan términos de suavidad para evitar predicciones de profundidad muy “ruidosas” y pérdida de consistencia temporal.
        
    - **Ventajas**:
        - No se necesita “ground truth” de profundidad.
        - Se puede entrenar simplemente con vídeos “sin etiquetar” (por ejemplo, un dron que recorra una escena).
            
    - **Desventajas**:
        
        - El método asume que la escena es estática (no hay objetos en movimiento).
            
        - Puede haber ambigüedad de escala (la red aprende profundidad relativa, y no siempre sabe si la escena es de “metro” o “kilómetro”).
            
        - Funciona peor cuando la cámara no se mueve o se mueve muy poco.
            
2. **Estéreo auto-supervisado**
    
    - **Idea**: Si tengo pares estéreo ($I_L$, $I_R$) sin mapas de profundidad, puedo entrenar una red que prediga disparidad $\hat{d}(x,y)$, y al reproyectar $I_L$ al punto correspondiente en $I_R$, minimizar la diferencia de apariencia entre la proyección y la vista real.
        
    - **Reproyección**:
        $$\hat{I}_R(x,y) = I_L\bigl(x + \hat{d}(x,y),\,y\bigr).$$
    - **Loss de apariencia**:
        $$\mathcal{L}_{\text{photo}} = \sum_{x,y} \rho\bigl(\,I_R(x,y) - \hat{I}_R(x,y)\bigr) + \rho\bigl(\,I_L(x,y) - \hat{I}_L(x,y)\bigr) ,$$
        donde $\rho$ es un terminu robusto (por ejemplo, error L1 o “SSIM”).
        
    - **Smoothness** + **Occlusion Handling**: Se incorporan máscaras para no penalizar píxeles ocluidos.
        
    - **Resultado**: Se aprende a predecir disparidad, que luego se convierte en profundidad con $Z(x,y) = \dfrac{B\,f}{\widehat{d}(x,y)}$.
        
    - **Pros y contras**:
        
        - Se aprovechan grandes cantidades de pares estéreo sin “ground truth”.
            
        - Requiere rigs estéreo calibrados (conoce $B$ y $f$).
            
        - Debido a oclusiones, regiones poco texturizadas o zonas saturadas, la predicción puede ser menos confiable que el método puramente supervisado.
            
3. **Redes preentrenadas “generalistas”**
    
    - **MiDaS (2020, 2021)**: Han reunido (fusionado) múltiples datasets con patrones distintos (escenas interiores, exteriores, ejemplos sintéticos…) y entrenaron un solo modelo que, sin calibración, genera un “mapa de profundidad relativo” con buena consistencia visual.
        
    - **LeReS (2021)**, **Boosting Monocular Depth**: refinar en diálogos iterativos y ajustes finos para distintas aplicaciones (AR, VR, robótica).
        

---

## Profundización en el concepto de “mapa de profundidad”

1. **¿Qué contiene un mapa de profundidad?**
    
    - Cada píxel $(x,y)$ de la imagen tiene asociado un valor $D(x,y)$ que corresponde a la distancia a la cámara. Por convención, si el cero del eje $z$ está en el plano de la cámara y el eje $z$ apunta hacia adelante, entonces:
        $$(x,y) > 0 \quad\text{si el objeto está “por delante” de la camara}$$
    - A menudo, los mapas de profundidad se normalizan a un rango $[0,1]$ para facilitar el entrenamiento, o a $[0,255]$ si se guardan como imágenes de 8 bits. En tal caso, la conversión al valor métrico real involucra linealmente un factor de escala:
        $$D_{\text{real}}(x,y) = D_{\text{norm}}(x,y) \times Z_{\max},$$
        
        donde $⁡Z_{\max}$ es la profundidad máxima plausible en el dataset (por ejemplo, 80 m en KITTI).
        
2. **Interpretación visual**
    
    - **Grises**: un píxel negro ($D=0$) indica que el objeto está en la posición de la cámara (o muy cerca), y un píxel blanco ($D=1$ o $D=255$) representa algo “muy lejos”.
        
    - **Falsos colores (colormaps)**: a menudo se usan paletas que van del azul (cercano) al rojo o violeta (lejano) para resaltar las variaciones y bordes de profundidad.
        
3. **Propiedades estructurales**
    
    - Un mapa de profundidad suele ser **suave** en superficies planas. Matemáticamente, donde la escena no cambia drásticamente, el gradiente espacial de $D(x,y)$ es pequeño:
        $$\bigl\|\nabla D(x,y)\bigr\| \;=\; \sqrt{\bigl(\partial_x D\bigr)^2 + \bigl(\partial_y D\bigr)^2} \quad\text{es reducido}.$$
    - En bordes de objetos, el mapa de profundidad puede presentar **discontinuidades** fuertes (por ejemplo, entre la silueta de una silla y el fondo).
        
    - Ciertos modelos (por ejemplo, los que usan pérdida de suavidad ponderada por el gradiente de la imagen) explotan la correlación entre los bordes de la imagen $I(x,y)$ y los bordes en el mapa de profundidad $D(x,y)$:
        $$\large{\bigl|\partial_x D(x,y)\bigr| \;\times e^{-\alpha\,|\partial_x I(x,y)|} \;+\; \bigl|\partial_y D(x,y)\bigr| \;\times e^{-\alpha\,|\partial_y I(x,y)|}}$$
        
        Cuando $\alpha$ es grande, se penaliza menos un gradiente de profundidad allí donde la imagen original (por ejemplo, el canal de luminancia) tiene un gradiente pronunciado, permitiendo discontinuidades en el contorno.
        

---

## ¿Cómo comenzar a investigar modelos de estimación de profundidad?

1. **Elección de un conjunto de datos (dataset)**
    
    - **KITTI Depth (2012, 2015)**: Conjunto de imágenes de carretera y escenas urbanas, con mapas de disparidad obtenidos por LiDAR y rig estéreo.
        
    - **NYU Depth v2**: Escenas interiores (hogar, oficina). Incluye imágenes RGB y mapas de profundidad (capturados con Kinect).
        
    - **Make3D**: Paisajes al aire libre, captura con un sensor específico para crear mapas de profundidad relativos.
        
    - **ETH3D**: Diferentes escenas con calibración precisa y mapas de profundidad densos.
        
    - **MegaDepth**: Generado automáticamente a partir de tours fotográficos en Internet; abarca escenas muy variadas (urbanas y exteriores).
        
2. **Selección de arquitectura base**
    
    - **Escoger un “backbone”** (por ejemplo, ResNet-50, EfficientNet-B5) como encoder.
        
    - **Diseñar un decoder** con upsampling paso a paso (un-pooling o convoluciones transpuestas), empleando skip-connections si se quiere preservar detalles espaciales.
        
    - Investigar modelos open-source (PyTorch, TensorFlow) como punto de partida:
        
        - [PyTorch Monodepth2](https://github.com/nianticlabs/monodepth2) (auto-supervisado con capacitación en vídeo).
        - [MiDaS en Torch Hub](https://github.com/isl-org/MiDaS) (para estimación monocular generalista).
            
3. **Preparación de datos y preprocesamiento**
    
    - Redimensionar todas las imágenes y mapas de profundidad a una resolución estándar (por ejemplo, $512\times256$ o $640\times360$).
        
    - Normalizar píxeles RGB (por ejemplo, restar media $[0.485,0.456,0.406]$, dividir por desviación estándar $[0.229,0.224,0.225]$).
        
    - Para el mapa de profundidad “ground truth”: convertirlo a rango $[0, 1]$ usando su profundidad máxima válida $D_{\max}$.
        
    - En entrenamiento auto-supervisado: generar secuencias consecutivas o pares estéreo para alimentar la red.
        
4. **Elección de la función de pérdida**
    
    - Si es supervisado: combinar $\mathcal{L}_1$ (o $\mathcal{L}_2$) con una pérdida de suavidad ($\mathcal{L}_{\text{smooth}}$). Por ejemplo:
        $$\mathcal{L} = \lambda_1 \,\mathcal{L}_1\bigl(\widehat{D},D\bigr) \;+\;\lambda_2\,\mathcal{L}_{\text{smooth}}\bigl(\widehat{D},I\bigr)$$
    - Si es auto-supervisado (monocular):
        $$\mathcal{L} = \lambda_{\text{photo}}\,\mathcal{L}_{\text{photo}} + \lambda_{\text{smooth}}\,\mathcal{L}_{\text{smooth}} + \lambda_{\text{consist}}\,\mathcal{L}_{\text{consistencia}}.$$
        - $\mathcal{L}_{\text{consistencia}}$ asegura que la profundidad predicha en $I_t$ y su reproyección a $I_{t'}$ concuerden.
            
5. **Entrenamiento y validación**
    
    - Dividir el dataset en entrenamiento, validación y prueba (por ejemplo, 80 % / 10 % / 10 %).
        
    - Monitorear métricas: $\text{AbsRel}$, $\mathrm{RMSE}$, $\delta < 1.25$.
        
    - Ajustar hiperparámetros ($\lambda$ en las pérdidas, tasa de aprendizaje, número de capas, tamaño de batch).
        
    - Para auto-supervisado: vigilar la **calidad visual** de los mapas de reproyección y la consistencia de la escena reconstruida.
        
6. **Prueba en el mundo real y generalización**
    
    - Idealmente, después de entrenar en un dataset específico, probar la red en imágenes “fuera de distribución” (otro conjunto de datos, otras condiciones de iluminación).
        
    - Si se necesita robustez, considerar usar preentrenamiento con múltiples datasets (transfer learning) o aplicar técnicas de **domain adaptation** (adaptación al dominio).
        

---

## Ejemplos de Arquitecturas Destacadas

A continuación, muestro tres ejemplos representativos de redes usadas en la literatura reciente para estimar mapas de profundidad monoscópicos.

---

### 1. **U-Net Modificado para Depth Estimation**

- **Encoder**:
    
    - ResNet-50 preentrenada en ImageNet.
        
    - Extrae características $\{f_1$, $f_2$, $f_3$, $f_4$, $f_5\}$ en distintas resoluciones:
        - $f_1$ tiene tamaño $H/2 \times W/2$,
        - $f_2$ tiene $H/4 \times W/4$, etc.
            
- **Decoder**:
    
    - Capas de “up-convolution” (convolución transpuesta) que van regresando a resolución plena $H \times W$.
        
    - En cada paso, hace _skip connection_ con $f_i$ para recuperar detalle espacial.
        
    - La salida final es un mapa de profundidad $\widehat{D}(x,y)$ con la misma dimensiones que la imagen de entrada (o ligeramente recortada).
        

**Ventajas**:

1. Fácil de implementar.
2. Conserva detalles de contorno gracias a los “skip connections”.
    

**Limitaciones**:

1. Si el dataset es “pequeño”, la red puede sobreajustarse.
2. No captura bien la consistencia a escala global si no se incluyen ramas de contexto más amplio.
    

---

### 2. **DORN: Deep Ordinal Regression Network**

- **Idea central**: En lugar de predecir un valor continuo de profundidad, discretiza el rango de distancias en $K$ “bins” ordenados $\{b_1, b_2, \dots, b_K\}$.
    
- **Predicción ordinal**: Para cada píxel, la red predice una distribución de probabilidad sobre los bins, de manera que si un píxel está más cerca, asigna mayor probabilidad a los bins cercanos; si está más lejos, a los bins lejanos.
    
- **Cálculo de profundidad final**:
    $$\widehat{D}(x,y) = \sum_{k=1}^K p_k(x,y)\,b_k,$$
    
    donde $p_k(x,y)$ es la probabilidad asignada al bin $b_k$.
    
- **Pérdida ordinal**: Se basa en comparar pares de bins y asegura que la red aprenda la ordenación correcta (es decir, si el píxel real pertenece al bin b5b_5, la red debería predecir que la probabilidad acumulada de los primeros 4 bins sea menor, etc.).
    

**Ventajas**:

- Mejora la estabilidad numérica al entrenar la regresión en un espacio ordinal.
- Suele tener menos error en zonas de transición de distancia (cambios abruptos).
    

**Desventajas**:

- Requiere diseñar un esquema de discretización (¿qué tan finos serán los bins?).
- Introduce hiperparámetros adicionales (número de bins, cómo normalizar).
    

---

### 3. **MiDaS: Mezcla de Datasets para Generación de Depth Maps (2020-2021)**

- **Enfoque principal**: Entrenar una única red en múltiples conjuntos de datos heterogéneos (indoor, outdoor, ciudades, automóviles, interiores, etc.) para que generalice mejor a imágenes del “mundo real” que no pertenezcan a ningún dataset específico.
    
- **Backbone**:
    
    - Usan una arquitectura de tipo encoder–decoder, con adaptaciones en el encoder para extraer representaciones más ricas en contextos variables.
        
    - Emplean “Feature Pyramid Networks” (FPN) para combinar información multiescala.
        
- **Pérdida**:
    
    - Como no hay un parámetro de escala único (cada dataset puede tener sus unidades de distancia diferentes), entrenan la red a **predecir un mapa de profundidad relativo** (una visualización consistente del relieve, más que valores absolutos).
        
    - Usan pérdida de entropía cruzada “ordinal” para clasificar cada píxel en un conjunto de rangos discretos relativos de profundidad (similar a DORN, pero adaptado a datos sin escala compartida).
        
    - Después, refinan con un conjunto de validación (fotos reales con LiDAR) para “alinear” la escala y el offset.
        

**Resultados**:

- MiDaS puede predecir mapas de profundidad de escenas arbitrarias (incluso fotografías de internet) con buena coherencia semántica: mesas, sillas, edificios y árboles se distinguen en la “forma” de la nube sin tener necesariamente la escala métrica correcta.
    

---

## Factores Prácticos para tu Investigación

1. **Disponibilidad de datos**
    
    - Si dispones de un rig estéreo (dos cámaras sincronizadas y calibradas), podrías explorar métodos auto-supervisados estéreo.
        
    - Si solo tienes una cámara monocular y ningún sensor extra (LiDAR, ToF), lo más probable es que optes por un método **monocular supervisado o auto-supervisado con vídeo**. En ese caso, necesitas:
        
        - Un dataset de vídeo monocular (para self-supervision), preferiblemente con cámara en movimiento.
            
        - **O** un dataset que ya contenga mapas de profundidad (p. e., NYU Depth, KITTI).
            
2. **Plataformas y frameworks**
    
    - La mayoría de implementaciones modernae se basan en **PyTorch** o **TensorFlow/Keras**.
        
    - Para auto-supervisado monocular te recomiendo revisar el repositorio de **Monodepth2** (Niantic, 2019) en PyTorch; ofrece ejemplos completos de entrenamiento y evaluación en KITTI.
        
    - Para un método “plug-and-play” generalista, puedes probar **MiDaS** (está empaquetado en Torch Hub y tiene instrucciones sencillas para obtener mapas de profundidad con una sola línea de código).
        
3. **Capacidad computacional**
    
    - Si tu GPU es limitada (o no tienes GPU), podrías entrenar primero en resoluciones reducidas (por ejemplo, $256\times128$) y usar un backbone relativamente pequeño (ResNet-18 en lugar de ResNet-50).
        
    - Alternativamente, entrenar con **transfer learning**: cargar pesos preentrenados en ImageNet (para el encoder), congelar las primeras capas y adaptar solo las últimas. Esto disminuye el tiempo de entrenamiento y la memoria requerida.
        
4. **Calibración y métricas**
    
    - Si necesitas profundidades métricas exactas (por ejemplo, para navegación de un robot), necesitarás calibrar la cámara muy bien (obtención precisa de la matriz intrínseca $K$, rectificación estéreo si hay dos cámaras, etc.).
        
    - Si tu objetivo es más estético o de segmentación (p. e., crear un desenfoque de fondo), bastará con un mapa de profundidad **relativa** (que solo preserve la jerarquía de cercanía/lejanía).
        

---

## Ejemplo Simplificado de Flujo de Trabajo (Metodología)

Para que tengas un esquema paso a paso de qué implicaría “investigar modelos de estimación de profundidad” en un proyecto práctico:

1. **Definición del problema y requisitos**
    
    - ¿Necesitas un mapa de profundidad real (en metros) o solamente uno relativo (para distinguir cerca/medios/lejos)?
        
    - ¿Dispones de imágenes aisladas, secuencias de vídeo, pares estéreo, o sensores ToF?
        
    - ¿Cuál es la resolución mínima aceptable para tu aplicación (¿128×128? ¿512×512? ¿Full HD?)?
        
2. **Selección del dataset**
    
    - Si no tienes tu propio rig estéreo o LiDAR, revisa los datasets públicos:
        
        - _Para interiores_: NYU Depth v2 (Kinect)
        - _Para exteriores/autos_: KITTI Depth
        - _Para escenas variadas_: MegaDepth, ETH3D, TUM RGB-D.
            
3. **Elección del enfoque**
    
    - **Supervisado monocular**: si tienes imágenes con “ground truth” de profundidad.
    - **Self-supervised monocular en vídeo**: si solo tienes vídeo monocular.
    - **Auto-supervised estéreo**: si tienes pares izquierdo/derecho calibrados.
    - **Sensores activos** (ToF): si puedes adquirir dispositivos como Intel RealSense u otro sensor.
        
4. **Implementación inicial**
    
    - Descarga un repositorio base (por ejemplo, Monodepth2 para self-supervision o MiDaS para un modelo generalista).
        
    - Ajusta hiperparámetros como tasa de aprendizaje ($\alpha$), pesos en la función de pérdida ($\lambda_{\text{photo}}$, $\lambda_{\text{smooth}}$), tamaño de batch, número de épocas.
        
    - Ejecuta pruebas de validación periódicas para asegurarte de que la red está aprendiendo (observa las métricas AbsRel, RMSE, etc.).
        
5. **Evaluación y análisis de resultados**
    
    - Visualiza algunos mapas de profundidad predecidos sobre imágenes de prueba. ¿Se ven coherentes? ¿Hay artefactos (zonas completamente negras o saturadas)?
        
    - Calcula métricas cuantitativas sobre un “test split” no visto.
        
    - Revisa casos límite: escenas con poca luz, mucho movimiento, superficies casi lisas.
        
6. **Mejoras iterativas**
    
    - Si observas parches oscuros (regiones sin detalle), tal vez necesites una penalización de suavidad más fuerte o agregar un módulo de atención para enfocarse en bordes.
        
    - Si la profundidad “se sale de escala” en imágenes de calles diversas, considera:
        
        - **Pre-entrenar** en MegaDepth para mayor diversidad.
            
        - Usar **fine-tuning** con un subconjunto doméstico (p. e., tu propio dataset con smartphone y sensor LiDAR si tienes acceso).
            
    - Si la red funciona bien en interiores pero mal en exteriores, quizás debas hacer **domain adaptation** o aumentar el dataset con datos sintéticos que cubran exteriores.
        
7. **Integración con el proyecto completo de AI**
    
    - **Salida del depth map** → componente posterior (por ejemplo, segmentación semántica 3D, navegación, reconstrucción 3D).
        
    - Ajustar el **pipeline** para que cada fotograma que ingresa a tu sistema pase primero por el “Depth Estimation Module” (estimación de profundidad) y entregue el mapa de profundidad a los módulos siguientes (detección de objetos 3D, path planning, etc.).
        
    - Optimizar el rendimiento en tiempo real (si la aplicación lo requiere):
        
        - Convertir la red a ONNX y ejecutar con TensorRT o OpenVINO.
            
        - Reducir la cuantización a 8 bits (pruning / quantization) para acelerar la inferencia en GPU o incluso en CPU.
            

---

## Conclusión

En el chat que compartió tu amigo, Jared te está asignando la tarea de **investigar “modelos de estimación de profundidad”**—es decir, algoritmos y redes neuronales que, dada una imagen o vídeo, produzcan un **mapa de profundidad** donde cada píxel indique la distancia desde la cámara hasta el objeto que ese píxel representa. Este “mapa de profundidad” es crucial en un gran abanico de proyectos de inteligencia artificial y visión por computador (desde robótica autónoma y realidad aumentada hasta reconstrucción 3D y fotografía computacional).

Para llevar a cabo esta investigación en profundidad, conviene:

1. **Comprender los fundamentos geométricos** (estéreo, SfM, calibración).
    
2. **Estudiar las técnicas clásicas** de correspondencia estéreo y algoritmos de triangulación.
    
3. **Adentrarse en los métodos de deep learning**, tanto supervisados (con datasets de imágenes + mapas de profundidad) como auto-supervisados (monocular en vídeo o estéreo sin etiquetas).
    
4. **Examinar papers de referencia** (Eigen et al., DORN, MiDaS, Monodepth2) para ver arquitecturas concretas, funciones de pérdida y resultados obtenidos sobre benchmarks estándar.
    
5. **Experimentar en la práctica**: escoger un dataset, configurar un pipeline de entrenamiento (encoder–decoder, losses de suavidad y ordinarización), evaluar métricas, ajustar hiperparámetros, y finalmente integrar la red en el sistema global de tu proyecto de AI.
    

Siguiendo estos pasos, tendrás un panorama teórico muy detallado, ejemplos concretos de architectures, loss functions, métricas de evaluación y, sobre todo, una guía práctica para poder **implementar, entrenar, evaluar y perfeccionar** un modelo de estimación de profundidad que genere mapas de profundidad de calidad para tu aplicación concreta. ¡Éxitos en tu investigación del “depth estimation”!