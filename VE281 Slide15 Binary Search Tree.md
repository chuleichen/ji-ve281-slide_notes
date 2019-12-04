## VE281 Slide15 Binary Search Tree

* Each node is associate with a key. (Assume all the keys are distinct)
* The key of any node is `greater` than the keys of all nodes in its `left` subtree and  `smaller` than the keys of all nodes in its `right` subtree.
* The average case time complexities for these operations are $O(\log n)$.

## Search 

```c++
struct node {
	Item item;
    node *left;
    node *right;
};

struct Item {
	Key key;
    Val val;
};

node *search(node *root, Key k) {
	if (root == NULL) return NULL;
    if (k == root->item.key) return root;
    if (k < root->item.key) return search(root->left, k);
    else return search(root->right, k);
}
```

## Insertion

```c++
void insert(node *&root, Item item) {
	if (root == NULL) {
    	root = new node(item);
        return;
    }
    if (item.key < root->item.key) insert(root->left, item);
    else if (item.key > root->item.key) insert(root->right, item);
}
```

## Removal

1. Node to be removed is a leaf: cut directly.
2. Node to be removed is a degree-one node: cut and connect to its child.
3. Node to be removed is a degree-two node: cut and replace by:
   * The largest node in its left subtree.
   * The smallest node in its right subtree.
   * Must be a leaf or a degree one node.

```c++
bool isLeaf(node *root) {
	if (root->right == NULL && root->left == NULL) return true;
    else return false;
}

node *&findMax(node *&root) {
	if (root->right == NULL) return root;
    return findMax(root->right);
}

void remove(node *&root, Key k) {
	if (root == NULL) return;
    if (k < root->item.key) remove(root->left, k);
    else if (k > root->item.key) remove (root->right, k);
    else {//root->item.key == k
     	  //remove a leaf
			if (isLeaf(root)) {
        		delete root;
            	root = NULL;
       		} else { //remove degree-one or two node
            	if (root->right == NULL) { //no right child
                	node *tmp = root;
                    root = root->left;
                    delete tmp;
                } else if (root->left == NULL) { //no left child
                	node *tmp = root;
                    root = root->right;
                    delete tmp;
                } else { //remove degree-two node
                	node *&replace = findMax(root->left);
                    root->item = replace->item;
                    node *tmp = replace;
                    replace = replace->left; 
                    	//bot leaf and degree-one node are OK;
                    delete tmp;
                }
            }
         }
} 
```



