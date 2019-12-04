# VE281 Slide16 Average-Case Time Complexity of BST

* The depth of the BST is $h$, the number of nodes is $n$. The time complexity for a **successful** search: 

  * In the worst case, $O(h)$, $O(n)$.
  * In the average case, $O(h)$.

* The successful search reaches a node at level $d$, the number of nodes visited is $d+1$, the complexity is $\Theta(d)$.

* Assume that it is equally likely for the object of the search to appear in any node of the search tree. The average complexity is $\Theta(\bar{d})$. $\bar{d}$ is the average depth of the nodes in a given tree.
  $$
  \bar{d} = \frac{1}{n} \sum_{i = 1}^nd_i
  $$

  * $\sum_{i=1}^nd_i$ is called internal path length.
  * Define the **average internal path length** of a tree containing $n$ nodes as $I(n)$. $I(1) = 0$.
  * For a tree of $n$ nodes, suppose it has $n$ nodes in its left subtree. $T(n; l) = I(l) + I(n-1-l) + n-1$.
  * $I(n) = \frac{1}{n}\sum_{l=0}^{n-1}T(n;l) = \frac{2}{n}\sum_{l=0}^{n-1}I(l)+(n-1)$.

* $I(n) = O(n\log n)$ and the average complexity for a successful search is $O(\log n)$.

* The average-case time complexity for an unsuccessful search is $O(\log n)$.

* Given $n$ nodes, the average-case time complexities for `search`, `insertion`, and `removeal` are all $O(\log n)$.

