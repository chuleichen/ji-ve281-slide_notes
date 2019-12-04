# VE281 Slide13 Binomial Heaps

* `Make-Heap()`: create an empty heap
* `Insert(H,x)`: insert an element `x` into the heap
* `Extrat-Min(H)`: remove and return an element with the smallest key.
* `Decrease-Key(H, x, k)`: decrease the key of element `x` to `k`.
* `Is-Emoty(H)`: is the heap empty
* `Find-Min(H)`: return an element with smallest key
* `Delete(H, x)`: delete element `x` from the heap
* `Union(H1, H2)`: replace heaps `H1` and `H2` with their union



## Binary Heap

* Height of complete binary tree with $n$ nodes is $\lfloor \log_2 n \rfloor$.
* Pointer representation: each node has a pointer  to parent and two children
  * Number of elements $n$.
  * Pointer to root node.
  * Find pointer to last node or next node in $O(\log n)$ time.
* Array representation: Indexes start at **1**.
  *  Take nodes in **level** order.
  * Parent of node $k$ is at $\lfloor k/2 \rfloor$.
  * Children of node at $k$ are at $2k$ and $2k+1$.

1. `insert`
   1. Add element in new node at end.
   2. Repeatedly exchange new element with element in its parent until heap order is restored. (`perculateUp`)
2. `Extract_min`
   1. Exchange element in root node with last node.
   2. Repeatedly exchange element in root with its smaller child until heap order is restored. (`perculateDown`)
3. `Decrease_key`
   1. Change the key.
   2. `perculateUp`

* In an implicit binary heap, any sequence of $m$ `Insert`, `Extract-min` and `Decrease-key` operations with $n$ `Insert` operations takes $O(m\log n)$ time.
* In an explicit binary heap with n nodes, the operations  `Insert`, `Extract-min` and `Decrease-key` take O(log n) time in the worst case.

4. `Find_min`: return element in the root node.
5. `delete`
   1. Exchange the node with last node.
   2. `perculateUp` or `perculateDown`
6. `union`: Given two binary heaps H~1~ and H~2~, merge into a single binary heap. Requires $\Omega(n)$ time. 
7. `heapify`:  Given $n$ elements, can construct a binary heap containing those n elements in $O(n)$ time. (Bottom-up)



## d-ary heap

* Empty or node with links to $d$ disjoint d-ary trees.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-15%20162001.png?raw=true)



## Binomial Heap

* A binomial tree of order $k$ is defined recursively: 

  * Order $0$: single node.
  * Order $k$: one binomial tree of order $k-1$ linked to another of order $k-1$.

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-15%20162934.png?raw=true)

* Given an order $k$ binomial tree $B_k$

  * Height: $k$.
  * Nodes: $2^k$.
  * It has $\left( \begin{matrix} k \\ i \end{matrix} \right)$ nodes at depth $i$.
  * Degree of its root: $k$.
  * Deleting its root yields $k$ binomial trees $B_{k-1}, \cdots, B_0$.
    ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-15%20163321.png?raw=true)

* A binomial heap is **a sequence of** binomial trees such that

  * Each tree is min-heap ordered.
  * There is either 0 or 1 binomial tree of order $k$.

* Represent trees using **left-child**, **right sibling** pointers.

* The roots of trees connect with **singly-linked list**, with degrees decreasing from left to right.

* `union`

  * Both order $k$:

    * Connect roots of H~1~ and H~2~.
    * Choose node with smaller key to be root of H.

    ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-15%20163842.png?raw=true)

  * Different order:
    ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-15%20164033.png?raw=true)

  * Time complexity: $O(\log n)$

* `Extrct_min`

  1. Delete the node with minimum key in binomial heap H.
  2. Union the origin binomial tree and the broken binomial tree.

* `Decrease_key`

  1. Change the key.
  2. `perculateUp`

* `delete`

  1. `Decrease_key(H, x, -inf)`
  2. `Delete-min(H)`

* `insert`

  1. Make a new tree with the element.
  2. Union the new tree and the origin tree

* In a binomial heap, the amortized cost of `insert` is $O(1)$ and the worst-case cost of `Extract-min` and `Decrease-key` is $O(\log n)$



## Summary

| operation     | linked list | binary heap | binomial heap |
| ------------- | ----------- | ----------- | ------------- |
| `makeHeap`    | $O(1)$      | $O(1)$      | $O(1)$        |
| `isEmpty`     | $O(1)$      | $O(1)$      | $O(1)$        |
| `insert`      | $O(1)$      | $O(\log n)$ | $O(1)$        |
| `extractMin`  | $O(n)$      | $O(\log n)$ | $O(\log n)$   |
| `decreaseKey` | $O(1)$      | $O(\log n)$ | $O(\log n)$   |
| `delete`      | $O(1)$      | $O(\log n)$ | $O(\log n)$   |
| `union`       | $O(1)$      | $O(n)$      | $O(1)$        |
| `findMin`     | $O(n)$      | $O(1)$      | $O(1)$        |

  