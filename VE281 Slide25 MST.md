# VE281 Slide25 MST

* **Minimum spanning tree**: Given a connected graph $G = (V, E)$ with real valued edge weights c~e~, and MST is a subset of the edges $T \subseteq E$ such that $T$ is a spanning tree whose sum of edge weights is minimized.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20161531.png?raw=true)
  * **Cayley's Theorem**: there are n^n-2^ spanning trees of K~n~.

## Greedy Algorithms

* Assume all edge costs c~e~ are distinct.

* **Cut property**: Let S be any subset of nodes, and let e be the min cost edge with exactly one endpoint in S. Then the MST contains e.

  * Cutset: A cut is a subset of nodes S. The corresponding cutset D is the subset of edges with exactly one endpoint in S.

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20162501.png?raw=true)

* **Cycle property**: Let C be any cycle, and let f be the max cost edge belonging to C. Then the MST does not contain f.

  * Cycle: Set of edges the form a-b, b-c, c-d, ..., y-z, z-a.

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20162516.png?raw=true)

* A cycle and a cutset intersect in an even number of edges.



* Kruskal's algorithm: Start with $T = \empty$, consider edges in ascending order of cost. Insert edge e in T unless doing so would create a cycle.

  1. Consider edges in ascending order of weight.

  2. If adding e to T create a cycle, discard 3 according to cycle property. 
     ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20170916.png?raw=true)

     Otherwise, insert e = (u, v) into T according to cut property where S = set of nodes in u's connected component.
     ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20170930.png?raw=true)

  * Algorithm:
    ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20171055.png?raw=true)
  * Time complexity: $O(m \log n)$ for sorting and $O(m\ \alpha(m,n))$ for union-find.

* Reverse-Delete algorithm: Start with $T = E$. Consider edges in descending order of cost. Delete edge e from T unless doing so will disconnect T.

* Prim's algorithm: Start with some root node s and greedily grow a tree T from s outward. At each step, add the cheapest edge to T that has exactly one endpoint in T.

  1. Initialize S = any node.
  2. Apply cut property to S.
  3. Add min cost edge in cut set corresponding to S to T, and add one new explored node u to S.
     ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20170207.png?raw=true)

  * Algorithm:
    ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-27%20170501.png?raw=true)
  * Time complexity: $O(n^2)$ with an array, $O(m\log n)$ with a binary heap.