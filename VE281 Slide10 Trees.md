# VE281 Slide10 Trees

  

## Trees

* An extension of linked list data structure whose node connects to multiple nodes.
* The node at the top of the hierarchy is the `root`.
* Nodes are connected by `edges`.
* Edges define `parent-child` relationship.
* A node with no children is called a `leaf`.
* `Subtrees` can be define for any node in general.
* Nodes that share the same parent are `silbings`.
* A `path` is a sequence of nodes such that the next node in the sequence is a child of the previous.
* `Path length` may be 0. (go to its own)
* If there exists a path between two nodes, then the path is `unique`.
* If there exists a path from node A to a node B, then A is an `ancestor` of B and B is a `descendant` of A.
* The `depth` or `level` of a **node** is the length of the unique path from the `root` to the node.
* The `height` of a **node** is the length of the `longest` path from the node to a `leaf`.
* The `height` of a **tree** is the height of its root. This is also know as the `depth` of a **tree**.
* The `number of levels` of a **tree** is the height of the tree **plus one**.
* The `degree` of a **node** is the number of children of a node.
* The `degree` of a **tree** is the maximum degree of a node in the tree.

## Binary Trees

* Every node can only have at most two children.

* An empty tree is a special binary tree.

* The **minimum** number of nodes in a binary tree of height `h`: $h+1$.

* The **maximum** number of nodes in a binary tree of height `h`: $2^{h+1}-1$.

* Given height `h`: $h+1 \leq n \leq 2^{h+1}-1$

* Given number of nodes `n`: $\log_2(n+1)-1 \leq h \leq n-1$.

* A binary tree is `proper` is every node has 0 or 2 children.

* A binary tree is `complete` if 

  * every level **except** the lowest is fully populated.
  * the lowest level is populated from left to right.

* A binary tree is `perfect` if every level is fully populated.

* Numbering nodes in a perfect binary tree: $1$ to $2^{h+1} -1$, from top to bottom, from left to right:
  <img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide10%20Trees.assets%5C%E6%89%B9%E6%B3%A8%202019-10-28%20154542.png" alt="批注 2019-10-28 154542" style="zoom:50%;" />

  * Parent of node $i$: $\lfloor i/2 \rfloor$.
  * Left child of node $i$: $2i$.
  * Right child of node $i$: $2i+1$.

* Representing binary tree using array: based on  a perfect binary tree.

* Linked structure

  ```c++
  struct node {
      Item item;
      node *left;
      node *right;
  };
  ```

  `left`/`right` points to a left/right **subtree**, `NULL` if empty. For a leaf node, both `left` and `right` point to NULL.