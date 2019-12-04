# VE281 Slide17 Binary Search Tree Additional Operations

| operation                 | time complexity |
| ------------------------- | --------------- |
| Search                    | $O(\log n)$     |
| Insert                    | $O(\log n)$     |
| Remove                    | $O(\log n)$     |
| Output in Sorted Order    | $O(n)$          |
| Get Min/Max               | $O(\log n)$     |
| Get Predecessor/Successor | $O(\log n)$     |
| Rank Search               | $O(\log n)$     |
| Range Search              | $O(n)$          |

* Output in Sorted Order: in-order depth-first traversal

* Get Min/Max:

  1. Start at root.
  2. Follow left/right child point until cannot go anymore.
  3. Return the last key found.

* Get Predecessor/Successor

  * Predecessor: the node with the largest key that is smaller than the current key. (max key in left subtree)
  * Successor: the node with the smallest key that is larger than the current key. (min key in right subtree)

* Rank Search: the index of the key in the ascending order (assume the smallest key gas rank 0).

  * Keep counting during an in-order depth-first traversal.
  * `leftSize`: the number of nodes in its left subtree.
  * `x.leftSzize` = the rank of `x` in the tree rooted at `x`.

  ```c++
  node *rankSearch(node *root, int rank) {
      if (root == NULL) return NULL;
      if (rank == root->leftSize) return root;
      if (rank < root->leftSize) return rankSearch(root->left, rank);
      else return rankSearch(root->right, rank - 1 - root->leftSize);
  }
  ```

* Range Search: find all items whose keys fall between  a range of values, inclusive, in sorted order.

  1. If search range covers all or part of left subtree, search left. (recursive)
  2. If root is in search range, add root to results.
  3. If search range covers all or part of right subtree, search right. (recursive)

  `void rangeSearch(node *root, Key searchRange[], Key treeRange[], List results)`