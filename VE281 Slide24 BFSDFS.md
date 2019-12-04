# VE281 Slide24 BFSDFS

## Exploring Graphs

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20200253.png?raw=true)

* Every node it visits must be reachable from v.
* Every node reachable from v must be visited.

## Depth-First Search

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20200724.png?raw=true)

* Every edge is examined exactly twice.
* Run time complexity: $O(|V| + |E|)$.
* Connectivity in Undirected Graphs:
  * Assign each node v and integer `CCNUM[v]` to identify the connected component to which it belongs.
    `PREVIST(v)`
    `CCNUM[v]=cc`
  * Initially, cc = 0. And will increase each time `DFS` calls `EXPLORE`. 
* Previsit and postvisit orderings
  * For each node, we will note down the times of two important events:
    * the moment of first discovery.
    * and the moment of final departure.
  * `PREVISIT(v)`
    `PRE[v] = clock`
    `clock = clock + 1`
  * `POSTVISIT(v)`
    `POST[v] = clock`
    `clock = clock + 1`
  * $\forall u, v \in V$, intervals $[PRE(u), POST(u)]$, $[PRE(v), POST(v)]$ are either **disjoint** or **one is contained within the other**.

### Search Tree/Forest

* **Tree edges**: part of the DFS forest. `PRE`/`POST`ordering for (u, v)
* **Forward edges**: [~u~ [~v~    ]~v~ ]~u~ lead from a node to a non-child descendant in the DFS tree.
* **Back edges**: [~v~ [~u~    ]~u~ ]~v~ lead to an ancestor in the DFS tree.
* **Cross edges**: [~v~ ]~v~    [~u~ ]~u~ neither descendant nor ancestor. They lead to a node that has already been explored.
* A **directed** graph has a cycle if and only if its depth-first search reveals a back edge.
* Order the vertices such that every edge goes from a small vertex to a large one.
  * In a dag (directed and without a cycle), every edge leads to a vertices with a lower `POST` number.
  * Every dag has at least one **source** (with the lowest `POST` number, a node with no incoming edges) and at least one **sink** (with the highest `POST` number, a node with no outgoing edges).
    1. Find a source, output it, and delete it from the graph.
    2. Repeat until the graph is empty.





* Two nodes u and v of a **directed** graph are connected if there is a path from u to v and a path from v to u.
* This relation partitions V into disjoint sets that we call **strongly connected components**.
* Every directed graph is a dag of its strongly connected components.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20203909.png?raw=true)
* If the `EXPLORE` subroutine is started at node u, then it will terminate precisely when all nodes reachable from u have been visited. Therefore, if we call `EXPLORE` in a **sink strongly connected component**, then we will retrieve exactly that component.
* If C and C' are strongly connected components, and there is an edge from a node in C to a node in C', then the highest `POST` number in C is bigger than the highest `POST` number in C'.
* The node that receives the highest `POST` number in a depth-first search must lie in a source strongly connected component. The smallest `POST` number in a depth-first search may **NOT** lie in a sink strongly connected component.
* Explore numbers:
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20155614.png?raw=true)





## Breadth-First Search

* To find a node lies in a sink strongly connected component:
  * Consider the **reverse graph G^R^**, the same as G but all edges **reversed**.
  * Do a depth-first search of G^R^, the node with highest `POST` number will come from a source strongly connected component in G^R^, which is a sink strongly connected component in G.
* To continue once the first sink strongly connected component is discovered:
  * Once the first component is deleted, the node with the highest `POST` number among those remaining will belong to  a sink strongly connected component of whatever remain of G.

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20160432.png?raw=true)

* For each $d = 0, 1, 2, \cdots$, there is a moment at which
  * all nodes at distance $\leq d$ from s have their distances correctly set.
  * all other nodes have their distance set to $\infin$.
  * the queue contains exactly the nodes at distance $d$.
* Time complexity: $O(|V|+|E|)$.

