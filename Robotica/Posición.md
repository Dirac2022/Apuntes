
## Representación de la posición

En un plano bidimensional, la posición de un cuerpo rígido precisa de dos grados de libertad y, por tanto, la posición del cuerpo quedará definida por dos componentes independientes. En el caso de espacio tridimensional será necesario emplear tres componentes. En la figura, se representa el vector **p** en coordenadas cartesianas.

## Representación de la posición (Coordenadas Polares)

Para un plano, es posible también caracterizar la localización de un punto o vector $p$ respecto a un sistema de ejes cartesianos de referencia OXY utilizando las denominadas coordenadas polares $p(r, \theta)$.

En esta representación, $r$ representa la distancia desde el origen O del sistema hasta el extremo del vector $p$$, mientras que $\theta$ es el ángulo que forma el vector $p$ con el eje OX.


## Representación de la posición (Coordenadas Cilíndricas)

En el caso de tres dimensiones, un vector $p$ podrá expresarse con respecto a un sistema de referencia OXYZ, mediante las coordenadas cilíndricas $\mathbf{p}(r, \theta, z)$.

Las componentes $r$ y $\theta$ tienen el mismo significado que en el caso de coordenadas polares, aplicado el razonamiento sobre el plano OXY, mientras que la componente $z$ expresa la proyección sobre el eje OZ del vector $p$.


## Conversiones

**2 dimensiones: Cartesianas - Polares**

$$
\begin{cases} 
x = r \cos \theta \\ 
y = r \sin \theta 
\end{cases}
\quad
\begin{cases} 
r = \sqrt{x^2 + y^2} \\ 
\cos \theta = x/r, \; \text{sen} \theta = y/r, \; 0 \leq \theta < 2\pi 
\end{cases}
$$

**3 dimensiones: Cartesianas - Cilíndricas**

$$
\begin{cases} 
x = r \cos \theta \\ 
y = r \sin \theta \\ 
z = z 
\end{cases}
\quad
\begin{cases} 
r = \sqrt{x^2 + y^2} \\ 
\cos \theta = x/r, \; \text{sen} \theta = y/r, \; 0 \leq \theta < 2\pi \\ 
z = z 
\end{cases}
$$


## Representación de la posición (Coordenadas Esféricas)

- También es posible utilizar coordenadas **esféricas** para realizar la localización de un **vector en un espacio de tres dimensiones**.
- Utilizando el sistema de referencia OXYZ, **el vector p tendrá como coordenadas esféricas** $p(r, \theta, \phi)$, donde la componente **r** es la distancia desde el origen $O$ hasta el extremo del vector **p**; la componente $\theta$ es el ángulo formado por la proyección del vector **p** sobre el plano OXY con el eje OX; y la componente **φ** es el ángulo formado por el vector **p** con el eje OZ.

**Condiciones:**
- $0 \leq \theta < 2\pi$
- $0 \leq \phi \leq \pi$
- $r \geq 0$


### Conversiones (Cartesianas - Esféricas)

$$
\begin{cases} 
x = r \text{ sen } \phi \text{ cos } \theta \\ 
y = r \text{ sen } \phi \text{ sen } \theta \\ 
z = r \text{ cos } \phi 
\end{cases}
$$

$$
\begin{cases} 
r = \sqrt{x^2 + y^2 + z^2} \\ 
\text{sen } \phi = \frac{\sqrt{x^2 + y^2}}{r}, \text{cos } \phi = \frac{z}{r}, \quad 0 < \phi < \pi \\ 
\text{sen } \theta = \frac{y}{r \text{ sen } \phi}, \text{cos } \theta = \frac{x}{r \text{ sen } \phi}
\end{cases}
$$

---

<h5>Ejercicio 1</h5>

1. Hallar las coordenadas cilíndricas del punto A(–1, –1, 3)
2. Hallar las coordenadas cartesianas del punto A que tiene las coordenadas cilíndricas (2, $2\pi/3$$, –4)
3. Hallar las coordenadas cartesianas del punto A con coordenadas esféricas (4, $2\pi/3$$, $\pi/6$$)
4. Hallar las coordenadas esféricas del punto A con coordenadas cartesianas  
   $$ (-1/2, \sqrt{3}/2, \sqrt{3}) $$

**Respuestas:**
1. $(r, \theta, z) = \left( \sqrt{2}, \frac{5\pi}{4}, 3 \right)$$
2. $(x, y, z) = (-1, \sqrt{3}, -4)$$
3. $(x, y, z) = (-1, \sqrt{3}, 2\sqrt{3})$$
4. $(r, \theta, \phi) = (2, \frac{2\pi}{3}, \frac{\pi}{6})$$


<h5>Ejercicio 2</h5>

Un brazo robótico se mueve en el espacio tridimensional con una trayectoria determinada por las siguientes funciones paramétricas en coordenadas rectangulares:

$$
x(t) = \sin(t), \quad y(t) = \cos(t), \quad z(t) = t^2
$$

Donde $t$ es el tiempo.

1. Calcular la velocidad del brazo robótico en coordenadas rectangulares.
2. Convertir la velocidad a coordenadas cilíndricas y calcularla allí.
3. Convertir la velocidad a coordenadas esféricas y calcularla allí.
4. Evaluar y comparar los valores numéricos de las velocidades en $t = 1$$ para los tres sistemas de coordenadas (rectangulares, cilíndricas y esféricas).


<h5>Ejercicio 2 Sugerencias</h5>

**1. Coordenadas Rectangulares (Cartesianas)**

Dado un sistema paramétrico $(x(t), y(t), z(t))$$:

- **Velocidad v:**

$$
v = \left( \frac{dx}{dt}, \frac{dy}{dt}, \frac{dz}{dt} \right)
$$

<h5>2. Coordenadas Cilíndricas</h5>

Para un sistema paramétrico $(r(t), \theta(t), z(t))$$:

- **Conversión de Coordenadas Rectangulares a Cilíndricas:**

$$
r = \sqrt{x^2 + y^2}, \quad \theta = \text{atan} 2(y, x), \quad z = z
$$

- **Velocidad en Coordenadas Cilíndricas:**

$$
v_r = \frac{dr}{dt}, \quad v_\theta = r\frac{d\theta}{dt}, \quad v_z = \frac{dz}{dt}
$$

<h5>3. Coordenadas Esféricas</h5>

Para un sistema paramétrico $(r(t), \theta(t), \phi(t))$$:

- **Conversión de Coordenadas Rectangulares a Esféricas:**

$$
r = \sqrt{x^2 + y^2 + z^2}, \quad \theta = atan 2 (y, x), \quad \phi = atan 2 \left( \sqrt{x^2 + y^2}, z \right) 
$$

- **Velocidad en Coordenadas Esféricas:**

$$
v_r = \frac{dr}{dt}, \quad v_\theta = r \sin(\phi) \frac{d\theta}{dt}, \quad v_\phi = r \frac{d\phi}{dt}
$$

---

<h5>Ejercicio 2 Respuesta</h5>

**Velocidad (cartesianas):**
$$
v = (\cos(t), -\sin(t), 2t)
$$

**Velocidad (cilíndricas):**
$$
(v_r, v_\theta, v_z) = (0, -1, 2t)
$$

**Velocidad (esféricas):**
$$
(v_R, v_\theta, v_\phi) = \left( \frac{2t^3}{\sqrt{t^4 + 1}}, -1, -\frac{2t}{\sqrt{t^4 + 1}} \right)
$$

**Módulo |v| (cartesianas):**
$$
\sqrt{4t^2 + 1}
$$

**Módulo |v| (cilíndricas):**
$$
\sqrt{4t^2 + 1}
$$

**Módulo |v| (esféricas):**
$$
\sqrt{\frac{4t^6 + t^4 + 4t^2 + 1}{t^4 + 1}}
$$

**Evaluación en $t = 1$$ s (4 decimales):**
- **Cart:** (0.5403, -0.8415, 2.000)
- **Cil:** (0, -1.000, 2.000)
- **Esf:** (1.414, -1.000, -1.414)
- **Cart |v|:** 2.236
- **Cil |v|:** 2.236
- **Esf |v|:** 2.236

---
