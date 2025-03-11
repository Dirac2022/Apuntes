La computación gráfica es el campo de la informática visual, donde se utilizan computadoras tanto para generar imágenes visuales sintéticamente como integrar o cambiar la información visual y especial probada del mundo real.


# Pixels
- **spels**: spatial elements
- **pixels**: pictures elements
- **voxels**: volume elements


El **voxel** es la mínima unidad cúbica que forma parte de un objeto tridimensional. Digamos que es un pixel en 3D o un cubo en tres dimensiones que se usa para construir objetos en un espacio virtual.

![voxel.jpg (1121×663)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj5mJ24JVWreTygxiJmvcp_XmaKac9knlpkFazoVQcA_ISMhf_1FNDZeeqkmPuO3dCwi4tqFFVgjQ-hLw2-aZ03pb5HHfsFusi1BQUIUdyKIM2kz0Xg2VOGrbw2CmyVpuYKKb8IIdgcXiWm/s1600/voxel.jpg)


# Resolución espacial

La resolución espacial está asociada a la "densidad" de los pixeles de una imagen. La resolución espacial tiene que ver con la cantidad de píxeles por unidad de área.
- Una medida de resolución son los dpi "dots per inch"


# Distancia entre pixeles

![manhattan_distance.png (374×239)](https://uploads-cdn.omnicalculator.com/images/manhattan_distance.png?width=374&enlarge=0&format=webp)

Si tenemos dos píxeles $p$ y $q$ con coordenadas $(x, y)$ y $(s, t)$ entonces
## Distancia euclideana

$$
D_{\text{euc}} \ (p, q) = \sqrt{(x-s)^2 + (y-t)^2}
$$
## Distancia City-Block / Manhattan / D4

$$
D_{\text{cityblock}} \ (p, q) = |x-s| + |y-t|
$$

# Relación entre píxeles: vecindad

![a-vertical-and-horizontal-neighbor-b-diagonal-neighbors-and-c-8-pixel-neighbors.png (850×264)](https://www.researchgate.net/publication/359409095/figure/fig6/AS:1172855773511681@1656642015437/a-vertical-and-horizontal-neighbor-b-diagonal-neighbors-and-c-8-pixel-neighbors.png)

- El conjunto de los 4-vecinos de un pixel $\textbf{p}$ con coordenadas $(x, y)$ están dadas por $(x+1, y)$, $(x-1, y)$, $(x, y+1)$, $(x, y-1)$ y es denotado por $N_4(\textbf{p})$ 

- El conjunto de los vecinos diagonales de un pixel $\textbf{p}$ con coordenadas $(x, y)$ están dadas por $(x-1, y-1)$, $(x+1, y-1)$, $(x-1, y+1)$, $(x+1, y+1)$ y es denotado por $N_D(\textbf{p})$ 

- El conjunto de los 8-vecinos de un pixel $\textbf{p}$ con coordenadas $(x, y)$ están dadas por $N_4(\textbf{p}) \cup N_D(\textbf{p})$  


