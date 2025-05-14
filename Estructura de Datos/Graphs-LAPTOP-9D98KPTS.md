Intuitively, a graph is a collection of vertices (or nodes) and the connections between them.

**A simple graph** $G = (V, E)$ consists of a nonempty set $V$ of vertices and a possibly
empty set $E$ of edges, each edge being a set of two vertices from $V$. The number of vertices
and edges is denoted by $|V|$ and $|E |$, respectively.

**A directed graph**, or a digraph, $G = (V, E)$ consists of a nonempty set $V$ of vertices and a set $E$ of edges (also called arcs), where each edge **is a pair of vertices** from $V$.

**A multigraph** is a graph in which two vertices can be joined by multiple edges. A multigraph $G = (V,E,f )$ is composed of a set of vertices $V$, a set of edges $E$, and a function 
$f : E \to \{\{v_i, v_j\} : v_i, v_j \in V \text{ y } v_i \neq v_j\}$.

**A pseudograph** is a multigraph with the condition $vi ≠ vj$ removed, which allows for loops to occur; in a pseudograph, a vertex can be joined with itself by an edge.

**A complete graph** is a graph with $n$ vertices  and is denoted $K_n$ if for each pair of distinct
vertices there is exactly one edge connecting them.

**A subgraph** $G'$ of graph $G = (V,E)$ is a graph $(V',E')$ such that $V' ⊆ V$ and $E' ⊆ E$. 
**A subgraph induced** by vertices $V'$ is a graph $(V',E')$ such that every edges between the selected vertices $V'$ must be retained.

**A path** from $v_1$ to $v_n$ is a sequence of edges edge($v_1, v_2$), edge($v_2, v_3$), . . . , edge($v_{n-1}, v_n$)
and is denoted as path $v_1, v_2, v_3, . . . , v_{n–1}, v_n$. If $v_1 = v_n$ and no edge is repeated, then the path is called a **circuit**.

![[Examples of graphs.png]]
- (a-d) simple graphs
- (c) complete graph $K_4$
- (e) a multigraph
- (f) a pseudograph
- (g) a circuit in a graph
- (h) a cycle in a digraph


- **A graph is called a weighted graph** if each edge has an assigned number.
- Two vertices $v_i$ and $v_j$ are called **adjacent** if the $edge(v_i, v_j)$ is in $E$. 
- **The degree of a vertex** $v$, $deg(v)$, is the number of edges incident with $v$. 
- If $deg(v) = 0$, then $v$ is called an **isolated vertex**.


# Graph Representation

Given the graph
![[Graph representation.png]]

## Adjacency list
Specifies all vertices adjacent to each vertex of the graph.
![[Adjacency list representation I.png]]

![[Adjacency list representation II.png]]

## Adjacency matrix
An adjacency matrix of graph $G = (V,E)$ is a binary $|V| × |V|$ matrix such that each entry of this matrix
$$ a_{ij} \left\{ \begin{array}{lll} 1 \text{, if there exist and edge}(v_i, v_j)  \\ 
0 \text{, otherwise} \end{array} \right. $$
![[Adjacency matrix representation.png]]

### Incidence matrix
An incidence matrix of graph $G=(V,E)$ is a $|V|\times|E|$ matrix such that
	$$ a_{ij} \left\{ \begin{array}{lll} 1 \text{, if edge }e_j \text{ is incidendt with vertex}(v_i)  \\ 
		0 \text{, otherwise} \end{array} \right. $$
![[Incidency matrix representation.png]]


# Graph Traversals

## Depth-first search
Each vertex $v$ is visited and then each unvisited vertex adjacent to $v$ is visited. If a vertex $v$ has no adjacent vertices or all of its adjacent vertices have been visited, we backtrack to the
predecessor of $v$. The traversal is finished if this visiting and backtracking process leads
to the first vertex where the traversal started. If there are still some unvisited vertices in
the graph, the traversal continues restarting for one of the unvisited vertices.

![[Pasted image 20231212173110.png]]


![[Pasted image 20231212173210.png]]
This algorithm guarantees generating a tree (or a forest, a set of trees) that includes or spans over all vertices of the original graph. A tree that meets this condition is called a **spanning tree**. The algorithm does not include in the resulting tree any edge that leads from the currently analyzed vertex to a vertex already analyzed. As a result, certain edges in the original graph do not appear in the resulting tree. The edges included in this tree are called *forward edges or tree edges*, and the edges not included in this tree are called *back edges*.

The complexity of **depthFirstSearch()** is $O(||V| + |E|)$ 

## Breadth-first search


# Shortest Paths

## Dijkstra algorithm
A number of paths $p_1, ..., p_n$ from a vertex $v$ are tried, and each time, the shortest path is chosen among them, which may mean that the same path $p_i$ can be continued by adding one more edge to it. But if $p_i$ turns out to be longer than any other path that can be tried, $p_i$ is abandoned and this other path is tried by resuming from where it was left and by adding one more edge to it. Because paths can lead to vertices with more than one outgoing edge, new paths for possible exploration are added for each outgoing edge. Each vertex is tried once, all paths leading from it are opened, and the vertex itself is put away and not used anymore. After all vertices are visited, the algorithm is finished.
![[Pasted image 20231212192149.png]]


![[Pasted image 20231212192528.png]]

### Complexity of Dijkstra's algorithm
The complexity of Dijkstra’s algorithm is $O(|V|^2)$. The first for loop and the
while loop are executed |V| times. The efficiency can be improved by using a *heap* to store and order vertices and adjacency, using a heap turns the complexity of this algorithm into $O((|E|+ |V|) lg |V|)$.

Dijkstra's algorithm is not general enough in that it may fail when **negative weights** are used in graphs. To overcome this limitation, a *label-correcting method* is needed

## Ford Algorithm

![[Pasted image 20231214104130.png]]


# Cicle Detection
One algorithm to detecting cycles comes from the **depthFirstSearch()** , for undirected graphs with a small modification.

![[Pasted image 20231214105017.png]]

![[Pasted image 20231214105407.png]]



# Grafo Hamiltoniano
Un grafo hamiltoniano es un tipo especial de grafo en teoría de grafos que contiene un ciclo que visita cada vértice exactamente una vez. Este ciclo se llama ciclo hamiltoniano. Es similar al problema del agente viajero, donde se busca el ciclo hamiltoniano más corto en un grafo ponderado.