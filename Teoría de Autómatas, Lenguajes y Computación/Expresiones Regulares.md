
# Concatenación de lenguajes

\textbf{Definición:} Sea $L$ un lenguaje. Se cumple:
\[
L^0 = \{\varepsilon\}
\]
\[
L^n = L \circ L^{n-1} \quad \forall n \in \mathbb{N}
\]

\textbf{Propiedades:}
\begin{enumerate}
    \item $L^1 = L$
    \item $\phi^0 = \{\varepsilon\}$
    \item $\phi^n = \phi \quad \forall n \in \mathbb{N}$
\end{enumerate}

\textbf{Ejemplo:} Dado un lenguaje $L$ sobre el alfabeto romano, donde $L = \{u, v\}$:
\begin{align*}
    L^0 &= \{\varepsilon\} \\
    L^1 &= \{u, v\} \\
    L^2 &= L \circ L = \{uu, uv, vu, vv\} \\
    L^3 &= L \circ L^2 = \{uuu, uuv, uvu, uvv, vuu, vuv, vvu, vvv\}
\end{align*}

\section{Clausura de Lenguajes}

\textbf{Definición:} Dado un lenguaje $L$, se define la clausura de $L$, o simplemente clausura, como:
\[
L^* = \bigcup_{k=0}^{\infty} L^k = \{w_1 \cdots w_n / w_i \in L \land i \geq 0\}
\]
A $L^*$ se le llama la clausura de Kleene en honor al matemático lógico Stephen Cole Kleene.

\textbf{Clausura Positiva:} Dado un lenguaje $L$, la clausura positiva de $L$ es:
\[
L^+ = \bigcup_{k=1}^{\infty} L^k = \{w_1 \cdots w_n / w_i \in L \land i > 0\}
\]

\textbf{Ejemplo:} Dado $L = \{u, v\}$. Halle por extensión $L^*$ y $L^+$:
\[
L^* = \{\varepsilon, u, v, uu, uv, vu, vv, uuu, uuv, ...\}
\]
\[
L^+ = \{u, v, uu, uv, vu, vv, uuu, uuv, ...\}
\]

\textbf{Propiedades:}
\begin{enumerate}
    \item $L \subseteq L^+ \subseteq L^* \quad \forall L$
    \item $\varepsilon \in L^* \iff \varepsilon \in L$
    \item $\varepsilon \in L^* \quad \forall L$
\end{enumerate}

\section{Lenguajes Regulares}

\subsection{Aplicación}

Los lenguajes regulares pueden ser utilizados para especificar la generación de analizadores léxicos.

\subsection{Analizador Léxico}

Un analizador léxico es un programa que recibe como entrada el código fuente de otro programa (secuencia de caracteres) y produce una salida compuesta de lexemas. Las palabras están compuestas por lexemas y morfemas.

\textbf{Lexema:} Es la raíz o parte de la palabra que no varía.

Ejemplo:
\begin{itemize}
    \item \texttt{deport-} en \texttt{deporte}, \texttt{deportivo}, \texttt{deportista}
\end{itemize}

\textbf{Morfema:} Es la parte que se añade al lexema para completar su significado y para formar nuevas palabras.

Ejemplo:
\begin{itemize}
    \item \texttt{modern-} en \texttt{moderna}, \texttt{modernos}, \texttt{modernísimo}
\end{itemize}

\section{Expresiones Regulares}

Una expresión regular es una secuencia de caracteres que forma un patrón de búsqueda. Se usan para especificar un conjunto de cadenas requeridas para un propósito particular.

\subsection{Ejemplo:}

Dadas las cadenas \texttt{Handel}, \texttt{Händel} y \texttt{Haendel}, el patrón sería:
\[
H(a|ä|ae)ndel
\]

\subsection{Definición:}

Una expresión regular es una forma de representar a los lenguajes regulares (finitos o infinitos) y se construye usando símbolos del alfabeto $\Sigma$ sobre el cual está definido el lenguaje.

\section{Abreviaturas}

Para los lenguajes listados a continuación se dan las abreviaturas correspondientes:

\begin{tabular}{|c|c|}
\hline
Lenguaje & Abreviatura \\
\hline
$\{v\} \cup \{w\}$ & $v \cup w$ \\
$\{vw\}$ & $vw$ \\
$\{w\}^*$ & $w^*$ \\
$\{w\}^+$ & $w^+$ \\
\hline
\end{tabular}

\end{document}
