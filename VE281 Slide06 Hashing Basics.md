# VE281 Slide06 Hashing Basics

## Hashing Basics

* Setup: A universe $U$ of objects
* Goal: maintain an evolving set $S \subseteq U$
* Array-based solution (index by $u \in U$): $\Theta(1)$ operation time, $\Theta(|U|)$ space.
* Linked list-based solution: $\Theta(|S|)$ space, $\Theta(|S|)$ operation time.
* Solution:
  1. Pick an array $A$ of $n$ buckets. $n = c|S|$: a small multiple of $|S|$.
  2. Choose a hash function: $h: U \rightarrow \{ 0, 1, \cdots , n - 1 \}$.
  3. Store item $k$ in $A[h(k)]$.
* The array is called **hash table**. An array of buckets, where each bucket contains item as assigned by a hash function. $h[k]$ is called the home bucket of key $k$.
* Collision occurs when the hash function maps two or more items with different search keys into the same bucket.

## Hash Function

* Design Criteria
  1. Must compute a bucket for every key in the universe.
  2. Must compute the same bucket for the same key.
  3. Should be easy and quick to compute.
  4. **Minimize collision**: completely random hashing (not feasible)
* Hash function: `h(key) = c(t(key))`
  1. Convert key into an integer: `t(key)` return an integer(**hash code**)
     * String: ASCII (add up | polynomial, a = 31 to minimize collisions, `hashCode()`)
     * Floating-point number: as a string of bits
     * Images, code snippets, Web site URL: bit-string, all of it or extracting parts
  2. Map an integer into a home bucket: `c(hashcode)` give an integer in the range $[0, n-1]$, where $n$ is the number of buckets in the table.
     * Modulo arithmetic: `homeBucket = c(hashcode) = hashcode % n`
     * Use odd `n` to make the hash uniform.
     * Use large prime number.

