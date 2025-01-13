




- [The Structure from Motion Pipeline](https://www.youtube.com/watch?v=i7ierVkXYa8&t=71s)
- [Overview | Structure from Motion - YouTube](https://www.youtube.com/watch?v=oIvg7sbJRIA&t=65s)
- 
# NeRF enable direct mapping of spatial

NeRF (Neural Radiance Fields) permitió crear una forma de "traducir" o "convertir" directamente:
- Las coordenadas espaciales (es decir, puntos en el espacio 3D representados por coordenadas x, y, z)
- En información sobre:
  1. Color (qué color tiene ese punto en el espacio)
  2. Densidad (qué tan "sólido" o "transparente" es ese punto)

Para entenderlo mejor, imagina que:
- Tienes un punto cualquiera en el espacio 3D
- NeRF puede decirte inmediatamente:
  - Qué color debería verse en ese punto exacto
  - Qué tan "denso" o "sólido" es ese punto (si es aire vacío, si es parte de un objeto sólido, etc.)

Esta capacidad fue revolucionaria porque permitió representar escenas 3D de una manera mucho más precisa y realista, ya que podía determinar exactamente cómo debería verse cada punto en el espacio.
# Radiancia
Un **valor de radiancia no negativo** es una medida cuantitativa de la luz que se emite o viaja desde un punto en una dirección específica en el espacio tridimensional. En términos más simples, describe la cantidad de luz que se observa desde un punto en una dirección dada, sin permitir valores negativos, ya que físicamente no tiene sentido tener "luz negativa".

### Conceptos clave:

1. **Radiancia**: Es una magnitud física que mide la cantidad de energía luminosa que pasa por una unidad de área en una dirección específica. Se expresa en unidades como W/m2⋅sr\text{W}/\text{m}^2\cdot\text{sr} (watts por metro cuadrado por estereorradián).
2. **No negativa**: Significa que el valor siempre es mayor o igual a cero. Esto refleja el hecho de que no puede haber emisión o propagación de "luz negativa"; si no hay luz, el valor será simplemente cero.

### Importancia:

En el contexto de los campos de radiancia, este valor no negativo garantiza que las simulaciones y las representaciones sean físicamente realistas. Por ejemplo:

- **Radiancia cero**: Indica que un punto no emite ni refleja luz en esa dirección.
- **Radiancia positiva**: Representa la cantidad de luz que un punto emite o refleja en una dirección específica.

Este principio asegura que los cálculos relacionados con iluminación y renderizado sigan las leyes físicas de la óptica, como la conservación de la energía luminosa.

# Structure-from-Motion (SfM)

La Structure from Motion (SfM) es una técnica de visión por computadora que reconstruye escenas 3D a partir de una secuencia de imágenes 2D en movimiento. 

## Principio Básico
La idea central es que cuando tienes varias imágenes de una escena tomadas desde diferentes puntos de vista, puedes:
- Reconstruir la estructura 3D de la escena
- Determinar el movimiento de la cámara (o las posiciones desde donde se tomaron las fotos)

## Proceso Principal

1. **Análisis de Imágenes**
   - Detecta puntos característicos en cada imagen
   - Busca coincidencias entre imágenes diferentes
   - Establece correspondencias entre estos puntos

2. **Reconstrucción**
   - Utiliza las correspondencias para calcular posiciones 3D
   - Determina la posición y orientación de la cámara
   - Crea una nube de puntos 3D

3. **Refinamiento**
   - Optimiza la reconstrucción
   - Mejora la precisión del modelo
   - Ajusta las posiciones de cámara

## Importancia
Es fundamental en muchas aplicaciones modernas:
- Modelado 3D
- Realidad virtual
- Mapeo y navegación robótica
- Preservación digital de patrimonio
- Efectos visuales en cine y medios

La SfM ha revolucionado cómo convertimos imágenes 2D en representaciones 3D útiles y precisas.


Imagina que tienes muchas fotos de un edificio tomadas desde diferentes ángulos. Structure from Motion es una técnica que permite:
1. Reconstruir el edificio en 3D
2. Determinar desde dónde se tomó cada foto

## Analogía Simple
Es similar a cómo nuestro cerebro funciona cuando caminamos alrededor de un objeto:
- Al movernos y ver el objeto desde diferentes ángulos
- Nuestro cerebro entiende su forma 3D
- También sabemos dónde estábamos parados en cada momento

## Cómo Funciona

| Paso | Descripción | Analogía |
|------|-------------|----------|
| 1. Detección de Puntos | Identifica puntos característicos en cada imagen | Como marcar puntos de referencia en el edificio |
| 2. Correspondencia | Encuentra los mismos puntos en diferentes imágenes | Reconocer que es el mismo punto desde diferentes ángulos |
| 3. Triangulación | Calcula la posición 3D de estos puntos | Como usar dos ojos para percibir profundidad |
| 4. Optimización | Refina la reconstrucción 3D y las posiciones de cámara | Ajustar nuestra percepción al ver más detalles |

## Aplicaciones Prácticas

1. **Fotografía y Video**
   - Creación de modelos 3D desde fotos
   - Efectos especiales en películas

2. **Arquitectura y Patrimonio**
   - Documentación de edificios históricos
   - Planificación de restauraciones

3. **Realidad Virtual/Aumentada**
   - Creación de entornos virtuales
   - Mapeo de espacios reales

4. **Robótica**
   - Navegación autónoma
   - Mapeo de entornos

## Ventajas y Limitaciones

### Ventajas
- Solo necesita fotos normales
- No requiere hardware especial
- Proceso automatizado

### Limitaciones
- Necesita texturas distintivas
- Puede fallar con superficies reflectantes
- Requiere suficiente superposición entre fotos

## Ejemplo Práctico
Imagina que quieres crear un modelo 3D de una estatua:
1. Tomas fotos alrededor de la estatua
2. El software identifica puntos comunes entre las fotos
3. Calcula la posición 3D de cada punto
4. Genera un modelo 3D completo
5. También te dice desde dónde se tomó cada foto


# Overview | Structure from Motion

Digamos que quieres cubrir la estructura tridimensional de esta estatua. Lo que haces es simplemente sacar tu celular y capturar un video de esta escultura simplemente caminando al rededor de ella. Esto se le conoce como un **video no controlado**. Es decir, no se conoce el movimiento de la cámara durante la captura del video. A partir de ese video se puede extraer tanto la estructura tridimensional de la escena como también el movimiento de la cámara a través del espacio. Esto es el problema **Structure-from-Motion**.