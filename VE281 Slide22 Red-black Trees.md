# VE281 Slide22 Red-black Trees

* Each node id either red or black.
* **Root rule**: the root is black.
* **Red rule**: red node can only have black children.
* **Path rule**: every path from a node  `x` to NULL must have the same number of **black** nodes (including `x` itself).
* **Black height** of a node `x` is the number of black nodes on the path form `x` to NULL, **including** `x` itself.
* If a red node has at least one child, it must have two children and they must be black.
* If a black node has only one child, that child must be a red leaf.
* Every red-black tree with $n$ nodes has height $\leq 2 \log_2(n+1)$.
* By **path rule**, every root-NULL path has $\leq \log_2(n+1)$ black nodes.
* By **red rule**, every root-NULL path has $\leq 2\log_2(n+1)$ total nodes.
* All **query operations** (e.g., search, min, max, succ, pred) work like general BST, and run in $O(\log n)$ time in the worst case.

## Insertion

* New node is always a red leaf.
  * If the parent is black, done.
  * If the parent is red: rotation or recoloring

### Violation at Leaf

* Assume `P` is the left child of the grandparent `G`. (right child case is symmetric)
* Three cases.

#### Q is a red leaf

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20192757.png?raw=true)

* Recoloring. (May recurse when G's parent is red.)

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20193053.png?raw=true)

#### Q is empty, I is P's left child

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20192817.png?raw=true)

* Right rotation.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20193151.png?raw=true)

* Recoloring.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20193202.png?raw=true)
* Done.

#### Q is empty, I is P's right child

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20192831.png?raw=true)

* Left rotation.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20193413.png?raw=true)
* The same as case 2.

### Violation at Internal Nodes

* Tree cases.

#### Q is a red node.

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20193920.png?raw=true)

* Recoloring.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20193958.png?raw=true)

* May recurse when G's parent is red.

#### Q is a black node, I is P's left child



![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20194125.png?raw=true)

* Right rotation.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20194138.png?raw=true)
* Recoloring.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20194155.png?raw=true)
* Done.

#### Q is a black node, I is P's right child

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20194327.png?raw=true)

* Left rotation.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-26%20194339.png?raw=true)
* The same as case 2.

### Violation Fix at the Root

* When the root is red.
* Color the root black.

### Runtime Complexity

* Rotation: $O(1)$.
* Recoloring: $O(\log n)$ in the worst case.
* Overall: $O(\log n)$.