# VE281 Slide07 Hashing: Collision Resolution

## Separate Chaining

* Each bucket keeps a linked list.
* `Value find(Key key)`, `k = h(key)`, search the linked list at the k-th bucket.
* `void insert(Key key, Value, value)`, search first, if found, update, if not, insert.
* `Value remove(Key key)`, search first, if found, remove the pair.

## Open Addressing

* Reuse empty space in the hash table to hold colliding items.
  1. **Probe** the hash table buckets mapped by h~0~(key), h~1~(key), ... , in sequence, until find an empty slot.
  2. Generally, define h~i~(x) = h(x) + f(i)
* Three methods:
  1. Linear probing: $h_i (x) = (h(x) + i) \% n$
  2. Quadratic probing: $h_i(x) = (h(x)+i^2)\%n$
  3. Double hashing: $h_i(x) = (h(x) + i * g(x)) \% n$



### Linear Probing

* $h_i(key) = (h(key) + i) \% n$

  ![](https://github.com/chuleichen/ji-ve281-slide_notes/blob/master/fig/%E6%89%B9%E6%B3%A8%202019-10-11%20162735.png?raw=true)
* `find()`: search by h~0~(key), h~1~(key) until find the key or an empty slot which means the key is not found.
* `remove()`: search and find the key and replace it with `del`
* Cluster problem: assuming input size N, table size 2N
  * Best case: 10101010
  * Worst case: 00111100
  * Time to find an empty slot:
    Good prob: 1
    Bad prob: 2, 3, ..., N + 1
    $E(prob) = \sum_{i = 1}^{2N}Pr(i)\cdot Probi = \sum_{i = 1}^N \frac{1}{2N} \cdot 1 + \sum_{i-1}^{N}\frac{1}{2N}(2 + 3 + \cdots + N+1) = \frac{N+5}{4}$

### Quadratic Probing

* $h_i(key) = (h(ley)+i^2)\%n$
* Less likely to form large clusters, but sometimes it is not able to find a slot even the table is not full.
* If the **load factor** $L = \frac{m}{n} = \frac{\#objects\ in\ hash\ table}{\#buckets \ in \ hash \ table} \leq 0.5$, we are guaranteed to find an empty slot.
* For open addressing, $L \leq 1$, and $L = O(1)$ is a necessary condition for operations to run in constant time.

### Double Hashing

* $h_i(x) = (h(x) + i*g(x)) \% n$
* Uses 2 distinct hash function, increment differently depending on the key.

### Performance of Open Addressing

* Hard to analyze rigorously.

* The runtime is dominated by the number of comparisons.

* The number of comparisons depends on the load factor $L$.

* Define the expected number of comparisons in an **unsuccessful search** as $U(L)$.

* Define the expected number of comparisons in a **successful search** as $S(L)$.

* Linear probing: 
  $$
  U(L) = \frac{1}{2}\left[ 1+(\frac{1}{1-L})^2\right] \\
  S{L} = \frac{1}{2}\left[ 1+\frac{1}{1-L}\right]
  $$
  $L \leq 0.75$ is recommended.

* Quadratic probing and double hashing:
  $$
  U(L) = \frac{1}{1-L} \\
  S(L) = \frac{1}{L} \ln \frac{1}{1-L}
  $$
  