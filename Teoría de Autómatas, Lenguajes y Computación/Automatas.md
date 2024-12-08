
# Autómatas con transiciones - $\varepsilon$



## $\varepsilon-clausura$
Para todo estado $s \in S$, definimos la $\varepsilon-clausura$ de $s$ como

$$
\text{clausura}_ε(s) = \{q \mid q \text{ es accesible desde } s \text{ sin consumir nada en la entrada}\}
$$

>[!info] Nota
>El estado $s$ pertenece a $clausura_\varepsilon (s)$


## Función de transición extendida
La función de transición extendida a cadenas se define mediante
$$
\begin{aligned}
\hat{\delta} (s, \varepsilon) &= clausura_\varepsilon  (s) \\
\hat{\delta} (s, ua) &= clausura_\varepsilon  (Q)
\end{aligned}
$$

donde 

$$
Q = \{q \mid \exists r \in \hat{\delta}(s, u) \land q \in \delta(r, a)\} \quad \forall u \in I^*, a \in I, s \in S
$$

$$
Q = \{q \mid   q \in \delta \, ( \, \hat{\delta}(s, u), a)\} \quad \forall u \in I^*, a \in I, s \in S
$$





El lenguaje aceptado por un $AFND-\varepsilon$  $M = (S, I, \delta, s^*, F)$ es el conjunto

$$
L(M) = \{ x / \hat{\delta} (s^*, x) \ \cap \ F \neq  \emptyset \}
$$

