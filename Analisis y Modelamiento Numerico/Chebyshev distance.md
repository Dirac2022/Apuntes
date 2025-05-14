
La distancia de Chebyshev entre dos puntos en un espacio multidimensional es la **mayor** de las diferencias absolutas entre sus coordenadas a lo largo de cualquier dimensión.

Formalmente, si tenemos dos puntos p=(p1​,p2​,...,pn​) y q=(q1​,q2​,...,qn​) en un espacio de n dimensiones, la distancia de Chebyshev entre ellos se define como:

DChebyshev​(p,q)=imax​{∣pi​−qi​∣}

En palabras más sencillas, calculas la diferencia absoluta entre las coordenadas correspondientes de los dos puntos para cada dimensión. Luego, la distancia de Chebyshev es el valor más grande de todas esas diferencias.

**Visualización en 2 Dimensiones (El Plano Cartesiano)**

Imaginemos que estamos en un plano cartesiano (2 dimensiones), donde cada punto tiene coordenadas (x,y). Sean dos puntos p=(x1​,y1​) y q=(x2​,y2​).

La distancia de Chebyshev entre p y q es:

DChebyshev​(p,q)=max{∣x1​−x2​∣,∣y1​−y2​∣}

Para visualizar esto, consideremos un punto de referencia, digamos el origen (0,0), y veamos qué puntos están a una distancia de Chebyshev constante de este origen.

**Gráfico 1: Puntos a una Distancia de Chebyshev de 1 del Origen**

Los puntos (x,y) que tienen una distancia de Chebyshev de 1 del origen (0,0) satisfacen max{∣x−0∣,∣y−0∣}=1, es decir, max{∣x∣,∣y∣}=1.

Esto significa que o bien ∣x∣=1 (y ∣y∣≤1), o bien ∣y∣=1 (y ∣x∣≤1). Los puntos que cumplen esta condición forman un cuadrado cuyos vértices son (1,1),(1,−1),(−1,1),(−1,−1).

```
      ^ y
      |
      1 +-------+
        |       |
       -1 +       + 1  > x
        |       |
      -1 +-------+
```

Todos los puntos dentro y sobre los bordes de este cuadrado tienen una distancia de Chebyshev menor o igual a 1 del origen.

**Gráfico 2: Puntos a una Distancia de Chebyshev de d del Origen**

Generalizando, los puntos (x,y) que tienen una distancia de Chebyshev de d del origen (0,0) satisfacen max{∣x∣,∣y∣}=d. Esto forma un cuadrado cuyos vértices son (d,d),(d,−d),(−d,d),(−d,−d).

```
      ^ y
      |
      d +-----------+
        |           |
       -d +           + d  > x
        |           |
      -d +-----------+
```

**Interpretación Geométrica**

La distancia de Chebyshev se puede interpretar como el número mínimo de movimientos que un rey en un tablero de ajedrez necesitaría para ir de una casilla a otra. El rey puede moverse una casilla en cualquier dirección: horizontal, vertical o diagonal.

Si consideramos dos puntos (x1​,y1​) y (x2​,y2​), la diferencia absoluta en las coordenadas ∣x1​−x2​∣ representa la distancia horizontal (o diagonal con un componente horizontal), y ∣y1​−y2​∣ representa la distancia vertical (o diagonal con un componente vertical). El rey siempre tomará el camino que maximice el movimiento en una sola dirección en cada paso.

**Ejemplo**

Consideremos los puntos p=(2,3) y q=(5,1).

La distancia de Chebyshev entre p y q es:

DChebyshev​((2,3),(5,1))=max{∣2−5∣,∣3−1∣}=max{∣−3∣,∣2∣}=max{3,2}=3

Esto significa que en un "tablero de ajedrez" donde p y q son casillas, un rey necesitaría 3 movimientos para ir de p a q. Un posible camino sería:

(2,3)→(3,2)→(4,1)→(5,1) (tres movimientos diagonales y uno horizontal).

**En Dimensiones Superiores**

El concepto se extiende a dimensiones superiores. En 3D, los puntos a una distancia de Chebyshev constante de un punto central formarían un cubo. En n dimensiones, formarían un hipercubo.

**En resumen:**

- La distancia de Chebyshev es la máxima diferencia absoluta entre las coordenadas de dos puntos.
- En 2D, los puntos a una distancia constante forman un cuadrado (rotado 45 grados con respecto a la distancia euclidiana).
- Se relaciona con el movimiento de un rey en un tablero de ajedrez.

Espero que esta explicación y las visualizaciones te hayan ayudado a comprender la distancia de Chebyshev. ¡No dudes en preguntar si tienes alguna otra duda!