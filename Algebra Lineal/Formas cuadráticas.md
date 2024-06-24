.ñ
# En $\mathbb{R}^n$
Una forma cuadrática de la forma $f(\textbf{x}) = \textbf{x}^TA\textbf{x}$, donde $A$ es una matriz simétrica de $n \times n$,se dice que es definida si toma solo un signo cuando $\textbf{x}$ varia sobre todos los vectores no nulos en $\mathbb{R}^n$. 

Una matriz real $A$ se dice que es 
- **Definida positiva** si $\textbf{x}^TA\textbf{x} > 0 \quad \: \forall \: \textbf{x} \in \mathbb{R}^n$
- **Definida negativa** si $\textbf{x}^TA\textbf{x} < 0 \quad \: \forall \: \textbf{x} \in \mathbb{R}^n$
- **Semidefinida positiva** si $\textbf{x}^TA\textbf{x} \geq 0 \quad \: \forall \: \textbf{x} \in \mathbb{R}^n$
- **Semidefinida negativa** si $\textbf{x}^TA\textbf{x} \leq 0 \quad \: \forall \: \textbf{x} \in \mathbb{R}^n$
- **Indefinida** si $\textbf{x}^TA\textbf{x}$ toma valores que difieren en el signo.



## Teorema
La forma cuadrática $f: \mathbb{R}^n \to \mathbb{R}$,  $f(\textbf{x}) = \textbf{x}^TA\textbf{x}$, en donde $A$ es una matriz simétrica, es definida positiva (definida negativa, semidefinida positiva, semidefinida negativa) si y solo si todos los valores propios de $A$ son positivos (negativos, no negativos, no positivos, respectivamente).

## Teorema
La forma cuadrática $f: \mathbb{R}^n \to \mathbb{R}$,  $f(\textbf{x}) = \textbf{x}^TA\textbf{x}$, en donde $A$ es una matriz simétrica, es definida positiva (definida negativa) si y solo si los [[Matrices#Menor principal de una matriz|menores principales]] son todos positivos (tienen signos alternados comenzando con $det(A_1) < 0$, respectivamente).
- A es semidefinida positiva si todos los menores principales (matrices esquina) son positivos
(no nulos) excepto el último que sea cero.
-  A es semidefinida negativa si todos los menores principales (matrices esquina) alternan de
signo iniciando por negativo (no nulos) excepto el último que sea nulo.
-  A es indefinida si el último menor es distinto de cero y la matriz A no es definida (positiva o
negativa).
-  A es indefinida si el último menor es cero, los demás menores son no nulos y la matriz A no
es semidefinida (positiva o negativa).
# En $\mathbb{C}$
Para el caso **complejo** una forma cuadrática tiene la forma $x^HAx$, el resultado de esta forma también es de naturaleza real. Es por eso que $x^HAx$ puede ser definida positiva, negativa o indefinida.

