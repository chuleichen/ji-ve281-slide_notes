# VE281 Slide21 AVL Trees

## Balanced Search Trees

* Balance: 

  * Height of a tree of `n` nodes  = $O(\log n)$

    * The height $h$ of an AVL balanced tree with $n$ internal nodes satisfies
      $$
      \log_2(n+1) - 1 \leq h \leq 1.44\log_2(n+2)
      $$
      

  * Balance condition can be maintain efficiently: $O(\log n)$ time to re-balance a tree.

* AVL tree: Adelson-Velsky and Landis' trees.

* Condition:

  * An empty tree is AVL balanced.
  * A non-empty binary tree is AVL balanced if
    1. Both its left and right subtrees are AVL balanced, and
    2. The height of left and right subtrees differ by at most 1.

## Rotation

* Right rotation:
  1. The right link of the left child becomes the left link of the parent.
  2. Parent becomes right child of the old left child.
     ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20161210.png?raw=true)

* Left rotation:

  1. The left link of the right child becomes the right link of the parent.
  2. Parent becomes left child of the old right child.

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20161351.png?raw=true)

* Balance Factor: $B_T = h_l - h_r$
* For every node `T` in the tree, $|B_T| \leq 1$.

### left left rotation

* Do a **right** rotation at node P.
* An **LL rotation** is called for when the node becomes unbalanced with a **positive** balance factor and the left subtree of the node also has a **positive** balance factor.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162053.png?raw=true)
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162108.png?raw=true)

### right right rotation

* Do a **left** rotation at node P.

* An **RR rotation** is called for when the node becomes unbalanced with a **negative** balance factor and the right subtree of the node also has a **negative** balance factor.

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162315.png?raw=true)
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162330.png?raw=true)


### left right rotation

* Do a **left** rotation on node A and then a **right** rotation on node P.

* An **LR rotation** is called for when the node becomes unbalanced with a **positive** balance factor but the left subtree of the node has a **negative** balance factor.

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162619.png?raw=true)
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162648.png?raw=true)
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162658.png?raw=true)

### right left rotation

* Do a **right** rotation on node A and then a **left** rotation on node P.
* An **RL rotation** is called for when the node becomes unbalanced with a **negative** balance factor but the right subtree of the node has a **positive** balance factor.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162939.png?raw=true)
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-25%20162954.png?raw=true)

* When the AVL tree becomes unbalanced after an insertion, exactly **one** single or double rotation is required to balance the tree.

## Supporting Data Members and Functions of AVL Tree

```c++
struct node {
    Item item;
    int height;
    node *left;
    node *right;
};

int Height(node *n) {
    if (!n) return -1;
    return n->height;
}

void AdjustHeight(node *n) {
    if (!n) return;
    n->height = max(Height(n->left), Height(n->right)) + 1;
}

int BalFactor(node *n) {
    if (!n) return 0;
    return (Height(n->left) - Height(n->right));
}

void LLRotation(node *&n);
void RRRotation(node *&n);
void LRRotation(node *&n);
void RLRotation(node *&n);

void Balance(node *&n) {
    if (BalFactor(n) > 1) {
        if (BalFactor(n->left) > 0) LLRotation(n);
        else LRRotation(n);
    }
    else if (BalFactor(n) < -1) {
        if (BalFactor(n->right) < 0) RRRotation(n);
        else RLRotation(n);
    }
}

void insert(node *&root, Item item) {
    if (root == NULL) {
        root = new node(item);
        return;
    }
    if (item.key < root->item.key) insert(root->left, item);
    else if (item.key > root->item.key) insert(root->right, item);
    Balance(root);
    AdjustHeight(root);
}
```

