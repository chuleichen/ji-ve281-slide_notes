# VE281 Slide12 Priority Queues and Heaps

## Priority Queue

* `isEmpty` , `size`, `getMin` : $O(1)$
* `enqueue`, `dequeMin`: $O(\log n)$

## Min Heap

* A binary heap is a **complete binary tree**

  * A min heap is a binary heap, and for any node `v`, the key of `v` is smaller than or equal to the keys of any **descendants*** of `v`.	(The key of the `root` of any subtree is always the smallest)

* Store the elements in an array in the order produced by a **level-order traversal**, the first element is stored at index **1**.
  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-11-13%20161732.png?raw=true)

  * A node at index $i$ ($i \not= 1$) has its parent at index $\lfloor i/2 \rfloor$.
  * A node at index $i (2i \leq n)$ has its left child at $2i$ and tight child at $2i+1$.

* Implementation: 

  * `isEmpty`: `return size == 0;`

  * `size`: `return size;`

  * `getMin`: `return heap[1];`

  * `enqueue`: 

    * `heap[++size] = newItem;`

    * `percoalteUp`

      ```c++
      void minHeap::percolateUp(int id) {
          while (id > 1 && heap[id/2] > heap[id]) {
              swap(heap[id], heap[id/2]);
              id = id/2;
          }
      }
      ```

    ```c++
    void minHeap::enqueue(Item newItem) {
        heap[++size] = newItem;
        percolateUp(size);
    }
    ```

  * `dequeueMin`

    * `swap(heap[1], heap[size--]);`

    * `percolateDown`

      ```c++
      void minHeap::percolateDown(int id) {
          for (j = 2 * id; j <= size; j = 2 * id) {
              if (j < size && heap[j] > heap[j + 1]) j++;
              if (heap[id] <= heap[j]) break;
              swap(heap[id], heao[j]);
              id = j;
          }
      }
      ```

    ```c++
    Item minHeap::dequeueMin() {
        swap(heap[1], heap[size--]);
        percolateDown(1);
        return heap[size + 1];
    }
    ```

  ## Min Heap Initialization and Application

  * Start at the rightmost array position that has a child (index $size/2$), percolate dawn all nodes in reverse level order.
  * Time complexity
    * Suppose the height of the heap is $h$.
    * Number of nodes at level $k (0 \leq k \leq h)$ is $2^k$.
    * The worst case time complexity of percolating down a node at level $k$ is $O(h - k)$. 
    * $T(h) \leq O(2^{h+1}-2-h)$, $h = \lfloor \log_2h \rfloor \leq \log_2 n$, $\Rightarrow T(n) = O(n)$.
  * Heap sort: Initialize a min heap ($O(n)$) and repeatedly call `dequeMin` ($O(n\log n)$)

