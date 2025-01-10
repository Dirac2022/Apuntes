

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

¿Te gustaría que profundice en algún aspecto específico de esta explicación?


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