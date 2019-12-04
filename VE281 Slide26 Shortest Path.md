# VE281 Slide26 Shortest Path

## Introduction to Shortest Path

### Definition

* Consider a digraph $G = (V, E)$ with edge-weight function $w: E \rightarrow R$, where $|V| = n$ and $|E| = m$. The weight of path $P = v_1 \rightarrow \cdots \rightarrow v_k$ is defined to be

$$
w(P) = \sum_{i = 1}^{k-1}w(v_i, v_{i+1})
$$

* A shortest path from $u$ to $v$ is a path of minimum weight from $u$ to $v$. The shortest path weight from $u$ to $v$ is defined as

$$
d(u,v) = min \{ w(P) |P \ is \ a \ path \ from \ u \ to \ v \}
$$

* $d(u,v) = +\infin$ if no pat from $u$ to $v$ exists.

### Property

* A subpath of a shortest path is a shortest path.
* If a graph G contains a negative-weight cycle, then some shortest paths may not exist.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide26 Shortest Path.assets\批注 2019-11-27 172326.png" alt="批注 2019-11-27 172326" style="zoom:50%;" />



## Single Source Shortest Path

### Definition

From a given source vertex $s \in V$, find the shortest-path weights $d(s,v)$ for **all** $v \in V$.

* If all edge weights $w(u, v)$ are nonnegative, all shortest-path weights must exist. (negative edge weights may lead to negative circle)
  * Nonnegative weight $\Rightarrow$ Dijkstra's Algorithm
  * Negative weight $\Rightarrow$ Bellman-Ford Algorithm



### Dijkstra's Algorithm

* Greedy algorithm

1. Maintain a set S of vertices whose shortest-path distances from s are known.
2. At each step add to S the vertex $v \in V-S$ whose distance estimate from s id minimal.
3. Update the distance estimates of vertices adjacent to v.

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide26 Shortest Path.assets\批注 2019-11-29 161603.png" alt="批注 2019-11-29 161603" style="zoom:50%;" />

* Initializing $d[s]\leftarrow 0$ and $d[v] \leftarrow + \infin$ for all $v \in V-{s}$ establishes $d[v] \geq d(s,v)$ for all $v \in V$, and this invariant is maintained over any sequence of relaxation steps.
* Dijkstra's algorithm terminates with $d[v] = d(s,v)$ for all $v \in V$.

| Implementation | `EXTRACT-MIN`                | `INSERT`/`DECREASE-KEY`     | N` $+ (|V|+|E|) \times$ ` `EXTRACT-MI$|V| \times$INS`/`DEC` |
| -------------- | ---------------------------- | --------------------------- | ----------------------------------------------------------- |
| Array          | $O(|V|)$                     | $O(1)$                      | $O(|V|^2)$                                                  |
| Binary Heap    | $O(\log|V|)$                 | $O(\log|V|)$                | $O(|V| + |E|) \log |V|$                                     |
| d-ary heap     | $O(\frac{d\log|V|}{\log d})$ | $O(\frac{\log|V|}{\log d})$ | $O(\frac{(d|V|+|E|)\log |V|}{\log d})$                      |
| Fibonacci Heap | $O(\log|V|)$ (amortized)     | $O(1)$ (amortized)          | $O(|V|\log |V| + |E|)$                                      |

* For unweighted graph: 
  * Use a FIFO queue instead of a priority queue. 
  * `v` comes after `u` in queue implies that $d[v] = d[u]$ or $d[v] = d[u] + 1$.
* If have a negative weight edges, do not have a chance to regret, which will lead to wrong answer.

### Bellman-Ford Algorithm

* Definition: a shortest path from u to v is a path of minimum weight from u to v. The shortest path weight from u to v is defined as
  $$
  d(u,v) = min\{w(P)|P \ is \ the \ path \ from \ u \ to \ v\}
  $$

* Definition: $OPT(i, u)$ is the length of the shortest $u-t$ path P using at most $i$ edges.

  * P uses at most $i-1$ edges: $OPT(i,u) = OPT(i-1, u)$.
  * P uses exactly $i$ edges: if $(u,v)$ is first edge, then OPT uses $(u,v)$, and then selects best $v-t$ path using at most $i-1$ edges.

  $$
  OPT (i,u) =  \left\{ \begin{matrix} 0 & if \ i = 0 \\ min\{ OPT(i-1, u), min_{(u,v) \in E}\{ OPT(i-1,v) + w(u,v) \} \} & otherwise \end{matrix} \right.
  $$

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide26 Shortest Path.assets\批注 2019-11-29 183722.png" alt="批注 2019-11-29 183722" style="zoom:50%;" />

* Time complexity: $O(mn)$.
* Space complexity: $O(n^2)$



* Maintain only one array $M[v]$ as shortest $v-t$ path found so far.

* No need to check edges of the form $(v,w)$ unless $M[w]$ changed.

* Throughout the algorithm, $M[v]$ is length of some $v-t$ path, and after $i$ rounds of updates, the value $M[v]$ is no larger than the length of the shortest $v-t$ path using $\leq i$ edges.

* Memory: $O(m+n)$

* Running time: $O(mn)$ in worst case, but substantially faster in practice.

  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide26 Shortest Path.assets\批注 2019-11-29 185321.png" alt="批注 2019-11-29 185321" style="zoom:50%;" />

* If $OPT(n,u) = OPT(n-1,u)$ for all $u$, then no negative cycles. If $OPT(n,u) < OPT(n-1,u)$ for some node $u$, then (any) shortest path from $u$ to $t$ contains a cycle $W$. Moreover $W$ has negative cost.
  
  * Can detect negative cost cycle in $O(mn)$ time: check if $OPT(n,u) = OPT(n-1,u)$ for all nodes $u$.

## All-Pair Shortest Paths

* Definition: Given Digraph $G=(V,E)$, where $|V| = n$, with edge-weight function $w:E \rightarrow R$, find $n \times n$ matrix of shortest path lengths $d(i,j)$ for all $i, j \in V$.
  * Bellman-Ford once from each vertex, $O(n^2m)$ time. ($O(n^4)$ for dense graph)

### Matrix Multiplication

* Consider the $n \times n$ adjacency matrix $A=(a_{ij})$ of the digraph, and define $d_{ij}^{(m)}$ as the weight of a shortest path from $i$ to $j$ that uses at most $m$ edges.

  * We have
    $$
    d_{ij}^{(0)} = \left\{  \begin{matrix} 0 & if \ i = j \\ \infin & if \ i \not = j \end{matrix} \right.
    $$
    and for $m = 1, 2, \cdots, n-1$
    $$
    d_{ij}^{(m)} = \min_k\{ d_{ik}^{(m-1)} + a_{kj} \}
    $$

  * $D^{(n-1)} = A^{(n-1)} = (d(i,j))$.

    * Time complexity: $\Theta(n^4)$.

  * Repeated squaring: $A^{2k} = A^k \times A^k$, compute $A^2, \cdots, A^{2\lceil \log_2(n-1) \rceil}$, $Time = \Theta(n^3 \log n)$.

    * Detect negative-weight cycles in $O(n)$ additional time.

### Floyd-Warshall Algorithm

* Define $c_{ij}^{(k)}$ as the weight of a shortest path from $i$ to $j$ with intermediate vertices belonging to the set $\{ 1, 2, \cdots, k \}$. Thus, $d(i,j) = c_{ij}^{(n)}$. Also, $c_{ij}^{(0)} = a_{ij}$.
  $$
  c_{ij}^{(k)} = \min_k \{ c_{ij}^{(k-1)}, c_{ik}^{(k-1)} + c_{kj}^{(k-1)} \}
  $$
  
* Algorithm: 
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide26 Shortest Path.assets\批注 2019-12-04 163319.png" alt="批注 2019-12-04 163319" style="zoom:50%;" />

* Time complexity: $\Theta(n^3)$.

* Transitive Closure of  a Directed Graph:

  * Compute:
    $$
    t_{ij} = \left\{  \begin{matrix} 1 & \text{if there exists a path from $i$ to $j$} \\ 0 & \text{otherwise} \\ \end{matrix} \right.
    $$

  * Use Floyd-Warshall, but use $(\vee, \wedge)$ instead of $(\min, +)$.
    $$
    t_{ij}^{(k)} = t_{ij}^{(k-1)} \vee (t_{ik}^{(k-1)} \wedge t_{kj}^{(k-1)})
    $$

  * Time complexity: $\Theta(n^3)$

### Johnson's Algorithm

* Given a label $h(v)$ for each $v \in V$, reweight each edge $(u,v)\in E$ by $\hat w(u,v) = w(u,v) + h(u) - h(v)$. Then, all paths between the same two vertices are reweighted by the same amount.

  * Find a vertex labeling $h$ such that $\hat w (u,v) \geq 0$ for all $(u,v) \in E$ by using Bellman-Ford to solve the difference constrains:
    $$
    h(u) - h(u) \leq w(u,v)
    $$
    or determine that a negative-weight cycle exists.

    * Time complexity: $O(mn)$

  * Run Dijkstra's algorithm from each vertex using $\hat w$.

    * Time complexity: $O(mn+n^2 \log n)$

  * Reweight each shortest-path length $\hat w(P)$ to produce the shortest-path lengths $w(P)$ of the original graph.

    * Time complexity: $O(n^2)$

  * Total time complexity: $O(mn+n^2 \log n)$