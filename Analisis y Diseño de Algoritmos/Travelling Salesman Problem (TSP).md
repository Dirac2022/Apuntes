El problema del agente viajero consiste en encontrar el camino más corto que recorre una serie de ciudades o puntos de interés vuelve al punto de partida, pasando por cada una de ellas exactamente una vez. El TSP es un problema de optimización clásico y se utiliza en una amplia variedad de aplicaciones, como la planificación de rutas de transporte, la distribución de productos o la localización de instalaciones. Algunas formas de resolver el TSP son:

- **Algoritmos exactos:** Estos métodos buscan la solución óptima de manera exhaustiva, pero suelen requerir mucho tiempo de cálculo y no son viables para problemas de gran tamaño.
- **Algoritmos heurísticos:** Estos métodos buscan soluciones aproximadas de manera más rápida, pero pueden no encontrar la solución óptima. Algunos ejemplos de algoritmos heurísticos para el TSP son el algoritmo de fuerza bruta, el algoritmo de construcción de vecino más cercano y el algoritmo de intercambio 2-opt.



# Dynamic Approach
https://www.baeldung.com/cs/tsp-dynamic-programming#:~:text=Dynamic%20Programming%20Approach%20for%20Solving%20TSP&text=If%20the%20number%20of%20cities,distance%20as%20a%20base%20case.&text=%2C%20then%20we'll%20calculate%20the,remaining%20cities%20is%20calculated%20recursively.

<div style="text-align: center;">
	<figure>
    <img src="https://www.baeldung.com/wp-content/uploads/sites/4/2020/10/1-3.png" alt="Texto alternativo de la imagen">
    <figcaption></figcaption>
    </figure>
</div>
 Let’s assume a salesman starts the journey from the city $A$. According to TSP, the salesman needs to travel all the cities exactly once and get back to the city ![A](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-816b613a4f79d4bf9cb51396a9654120_l3.svg "Rendered by QuickLaTeX.com") by choosing the shortest path.
# Procedimiento de ramificación y atadura

A través de este procedimiento dividimos el problema principal en diferentes subproblemas y encontramos una solución para cada uno de ellos por separado. Cabe señalar que una solución de un sub problema puede afectar a las soluciones de los siguientes subproblemas, debido al a ramificación del proceso.

# Procedimiento de fuerza bruta

Con este método primero calculamos y comparamos todas las rutas posibles para elegir una única solución en función de los destinos de la mercancía y demás consideraciones. Por tanto, finalmente se elegirá la ruta más corta considerada como la mejor.

# Procedimiento del vecino más próximo

Este procedimiento es el más simple y se trata de empezar a realizar el reparto desde el punto más cercano al conductor (agente viajero). No obstante, este método puede no ser el mejor para encontrar la ruta más óptima.