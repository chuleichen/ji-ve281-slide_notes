# VE281 Slide11 Binary Tree Traversal

* In a traversal, each node of the binary tree is visited **exactly once**.
* During the visit of a node, all actions with respect to this node are taken.

## Depth first traversal

### Pre-order

* Visit the node
* Visit its left subtree
* Visit its right subtree

```c++
void preOrder(node *n) {
    if (!n) return;
    visit(n);
    preOrder(n->left);
    preOrder(n->right);
}
```



![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-28%20161037.png?raw=true)

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-28%20161100.png?raw=true)

### Post-order

* Visit the left subtree
* Visit the right subtree
* Visit the node

```c++
void postOrder(node *n) {
    if (!n) return;
    postOrder(n->left);
    postOrder(n->right);
    visit(n);
}
```

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-28%20161309.png?raw=true)

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-28%20161323.png?raw=true)

### In-order

* Visit the left subtree
* Visit the node
* Visit the right subtree

```c++
void inOrder(node *n) {
    if (!n) return;
    inOrder(n->left);
    visit(n);
    inOrder(n->right);
}
```

## Level-Order Traversal

* Traverse the tree level by level from top to bottom.
* Within each level, traverse from left to right.

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-28%20161706.png?raw=true)

![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-28%20161722.png?raw=true)

1. Enqueue the root node to an empty queue.
2. While the queue is not empty, dequeue a node from the front of the queue.
   1. Visit the node.
   2. Enqueue its left child and right child into the queue.

```c++
void lelvelOrder(node *root) {
    queue q; //Empty queue
    q.enqueue(root);
    while (!q.isEmpty()) {
        node *n = q.dequeue();
        visit(n);
        if (n->left) q.enqueue(n->left);
        if (n->right) q.enqueue(n->right);
    }
}
```

