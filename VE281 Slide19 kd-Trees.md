# VE281 Slide19 kd-Trees

* At each level, keys from a different search dimension is used as the **discriminator**. (left $<$ and right $\geq$)

* Cycle through the dimensions as we go down the tree.

* `insert`: 

  ```c++
  void insert(node *&root, Item item, int dim) {
      if (root == NULL) {
          root = new node(item);
          return;
      }
      if (item.key == root->item.key) return; //equal in all dimensions
      if (item.key[dim] < root->item.key[dim]) 
          insert(root->left, item, (dim + 1) & numDim);
      else 
          insert(root->right, item, (dim + 1) & numDim);
  }
  ```

* `search`: 

  ```c++
  node *search(node *root, Key k, int dim) {
      if (root == NULL) return NULL;
      if (k == root->item.key) return root;
      if (k[dim] < root->item.key[dim]) 
          return search(root->left, k ,(dim + 1 % numDim));
      else 
          return search(root->right, k, (dim + 1) % numDim);
  }
  ```

* `remove`: 

  * If the node `R` to be removed has right subtree, find the node `M` in right subtree with the minimum value of the **current** dimension.
    1. Replace the value of R with the value of M.
    2. Recurse on M until a leaf is reached, then remove the leaf.
  * Else, find the node `M` in left subtree with the **maximum** value of the current dimension, then replace and recurse.

* `findMin`: 

  ```c++
  node *findMin(node *root, int dimCmp, int dim) {
      //dimCmp: dimension for comparison
      if (!root) return NULL;
      node *min = findMin(root->left, dimCmp, (dim + 1) % numDim);
      if (dimCmp != dim) {
          rightMin = findMin(root->right, dimCmp, (dim + 1) % numDim);
          min = minNode(min, rightMin, dimCmp);
      }
      return minNode(min, root, dimCmp);
  }
  ```

* `void rangeSearch(node *root, int dim, Key searchRange[], Key treeRange[], List results)`

  * `searchRange[]` holds two values (min, max) per dimension.
    * Min of dimension `j` at `searchRange[2 * j]`.
    * Max at `searchRange[2 * j + 1]`.
  * `treeRange[]` holds lower bound and upper bound per dimension for the tree rooted at `root`.
    * Update as go down the levels.
    * Check if a search range overlaps a subtree range.