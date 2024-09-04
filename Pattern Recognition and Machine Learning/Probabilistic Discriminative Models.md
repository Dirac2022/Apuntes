
# 4.2. Modelos Generativos Probabilísticos

A continuación, adoptamos una visión probabilística de la clasificación y mostramos cómo surgen los modelos con fronteras de decisión lineales a partir de suposiciones simples sobre la distribución de los datos. En la Sección 1.5.4, discutimos la distinción entre los enfoques discriminativos y generativos para la clasificación. Aquí adoptaremos un enfoque generativo en el que modelamos las densidades condicionales de clase $p(x|C_k)$, así como las probabilidades a priori de clase $p(C_k)$, y luego utilizamos estas para calcular las probabilidades posteriores $p(C_k|x)$ a través del teorema de Bayes.

Primero, consideremos el caso de dos clases. La probabilidad posterior para la clase $C_1$ se puede escribir como

$$
p(C_1|x) = \frac{p(x|C_1)p(C_1)}{p(x|C_1)p(C_1) + p(x|C_2)p(C_2)} = \frac{1}{1 + \exp(-a)} = \sigma(a) \tag{4.57}
$$

^579430

donde hemos definido

$$
a = \ln \frac{p(x|C_1)p(C_1)}{p(x|C_2)p(C_2)} \tag{4.58}
$$

y $\sigma(a)$ es la función sigmoide logística definida por

$$
\sigma(a) = \frac{1}{1 + \exp(-a)} \tag{4.59}
$$

que se muestra en la Figura 4.9. El término ‘sigmoide’ significa en forma de S. Este tipo de función a veces también se llama ‘función de aplastamiento’ porque mapea todo el eje real en un intervalo finito. La sigmoide logística ya se ha encontrado en capítulos anteriores y juega un papel importante en muchos algoritmos de clasificación. Satisface la siguiente propiedad de simetría

$$
\sigma(-a) = 1 - \sigma(a) \tag{4.60}
$$

como se verifica fácilmente. La inversa de la sigmoide logística está dada por

$$
a = \ln \left( \frac{\sigma}{1 - \sigma} \right) \tag{4.61}
$$

y se conoce como la función *logit*. Representa el logaritmo de la razón de probabilidades $\ln \left[ \frac{p(C_1|x)}{p(C_2|x)} \right]$ para las dos clases, también conocido como logaritmo de las probabilidades. Nótese que en [[#^579430|(4.57)]] simplemente hemos reescrito las probabilidades posteriores en una forma equivalente, por lo que la aparición de la sigmoide logística puede parecer un tanto vacía. Sin embargo, tendrá significancia siempre que $a(x)$ tome una forma funcional simple. Consideraremos en breve situaciones en las que $a(x)$ es una función lineal de $x$, en cuyo caso la probabilidad posterior está gobernada por un modelo lineal generalizado.

Para el caso de $K > 2$ clases, tenemos

$$
p(C_k|x) = \frac{p(x|C_k)p(C_k)}{\sum_{j} p(x|C_j)p(C_j)} = \frac{\exp(a_k)}{\sum_{j} \exp(a_j)} \tag{4.62}
$$

^3efc00

que se conoce como el exponencial normalizado y se puede considerar como una generalización multiclase de la sigmoide logística. Aquí las cantidades $a_k$ se definen por

$$
a_k = \ln p(x|C_k)p(C_k). \tag{4.63}
$$

El exponencial normalizado también se conoce como la función softmax, ya que representa una versión suavizada de la función ‘max’ porque, si $a_k \gg a_j$ para todo $j \ne k$, entonces $p(C_k|x) \approx 1$, y $p(C_j|x) \approx 0$.

Ahora investigamos las consecuencias de elegir formas específicas para las densidades condicionales de clase, mirando primero a las variables de entrada continuas $x$ y luego discutiendo brevemente el caso de entradas discretas.

![[figure 4.9.png]]
