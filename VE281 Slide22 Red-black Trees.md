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

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 192757.png" alt="批注 2019-11-26 192757" style="zoom:50%;" />

* Recoloring. (May recurse when G's parent is red.)

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 193053.png" alt="批注 2019-11-26 193053" style="zoom:50%;" />

#### Q is empty, I is P's left child

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 192817.png" alt="批注 2019-11-26 192817" style="zoom:50%;" />

* Right rotation.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 193151.png" alt="批注 2019-11-26 193151" style="zoom:50%;" />

* Recoloring.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 193202.png" alt="批注 2019-11-26 193202" style="zoom:50%;" />
* Done.

#### Q is empty, I is P's right child

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 192831.png" alt="批注 2019-11-26 192831" style="zoom:50%;" />

* Left rotation.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 193413.png" alt="批注 2019-11-26 193413" style="zoom:50%;" />
* The same as case 2.

### Violation at Internal Nodes

* Tree cases.

#### Q is a red node.

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 193920.png" alt="批注 2019-11-26 193920" style="zoom:50%;" />

* Recoloring.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 193958.png" alt="批注 2019-11-26 193958" style="zoom:50%;" />

* May recurse when G's parent is red.

#### Q is a black node, I is P's left child



<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 194125.png" alt="批注 2019-11-26 194125" style="zoom:50%;" />

* Right rotation.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 194138.png" alt="批注 2019-11-26 194138" style="zoom:50%;" />
* Recoloring.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 194155.png" alt="批注 2019-11-26 194155" style="zoom:50%;" />
* Done.

#### Q is a black node, I is P's right child

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 194327.png" alt="批注 2019-11-26 194327" style="zoom:50%;" />

* Left rotation.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide22 Red-black Trees.assets\批注 2019-11-26 194339.png" alt="批注 2019-11-26 194339" style="zoom:50%;" />
* The same as case 2.

### Violation Fix at the Root

* When the root is red.
* Color the root black.

### Runtime Complexity

* Rotation: $O(1)$.
* Recoloring: $O(\log n)$ in the worst case.
* Overall: $O(\log n)$.