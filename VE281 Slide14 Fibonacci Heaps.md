# VE281 Slide14 Fibonacci Heaps

## Time Complexity

| operation    | linked list | binary heap | binomial heap | Fibonacci heap |
| ------------ | ----------- | ----------- | ------------- | -------------- |
| Make Heap    | $O(1)$      | $O(1)$      | $O(1)$        | $O(1)$         |
| Is Empty     | $O(1)$      | $O(1)$      | $O(1)$        | $O(1)$         |
| Insert       | $O(1)$      | $O(\log n)$ | $O(\log n)$   | $O(1)$         |
| Extract Min  | $O(n)$      | $O(\log n)$ | $O(\log n)$   | $O(\log n)$    |
| Decrease Key | $O(1)$      | $O(\log n)$ | $O(\log n)$   | $O(1)$         |
| Delete       | $O(1)$      | $O(\log n)$ | $O(\log n)$   | $O(\log n)$    |
| Meld         | $O(1)$      | $O(n)$      | $O(\log n)$   | $O(1)$         |
| Find Min     | $O(n)$      | $O(1)$      | $O(\log n)$   | $O(1)$         |

* Starting from an empty Fibonacci heap, any sequence of $m$ `INSERT`, `EXTRACT-MIN`, and `DECREASE-KEY` operations involving $n$ `INSERT` operations takes $O(m + n log n)$ time.

## Structure

* Store a pointer to the minimum node.

* Maintain tree roots in a circular, doubly-linked list.

* Node representation:

  * A pointer to its parent
  * A pointer to any of its children
  * A pointer to its left and right siblings
  * Rank (number of children)
  * (whether it is marked)

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-20%20084240.png?raw=true)

* Notation:

  | notation | meaning                          |
  | -------- | -------------------------------- |
  | n        | number of nodes                  |
  | rank(x)  | number of children of node x     |
  | rank(H)  | max rank of any node in heap H   |
  | trees(H) | number of trees in heap H        |
  | marks(H) | number of marked nodes in heap H |

* Potential function: $\Phi(H) = treees(H) + 2 \cdot marks(H)$

## Implement

* `Insert`: 

  1. Create a new singleton tree.
  2. Add to root list.
  3. Update min pointer.

* `Extract Min`: 

  1. Delete min.
  2. Meld its children into root list.
  3. Update min.
  4. Consolidate trees so that no two roots have same rank.

  

  <img src="https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-20%20090918.png?raw=true" style="zoom: 50%;" />

* `Decrease Key`: 

  1. If heap order is not violated, decrease the key of x.
  2. Otherwise, cut tree rooted at x and meld into root list.
  3. If parent p of x is unmarked (hasn't yet lost a child), mark it.
  4. Otherwise, cut p, meld into root list and unmarked.
  5. Recursively do 3 - 4.

  

  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide14 Fibonacci Heaps.assets\批注 2019-11-20 091413.png" alt="批注 2019-11-20 091413" style="zoom:50%;" />

## Bounding the rank

1. Fix a point in time. Let x be a node of rank k, and let y~1~, …, y~k~ denote its current children in the order in which they were linked to x. Then, 
   $$
   rank(y_i) \geq \left\{ \begin{matrix} 0 & if \  i = 1 \\ i-2 & if \  i \geq 2 \end{matrix} \right.
   $$
   <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide14 Fibonacci Heaps.assets\批注 2019-11-20 091800.png" alt="批注 2019-11-20 091800" style="zoom:50%;" />

2. Let s~k~ be minimum number of elements in any Fibonacci heap of rank k. Then s~k~ $\geq$ F~k+2~, where F~k~ is the k^th^ Fibonacci number.

3. Let H be a Fibonacci heap with n elements. Then, rank(H) $\leq \log_{\Phi}$n, where $\Phi$ is the golden ratio = (1 + $\sqrt{5}$) / 2 $\approx$ 1.618.

