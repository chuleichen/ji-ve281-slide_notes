# VE281 Slide08 Hash Table Size, Rehashing, and Applications of Hashing

## Hash Table Size

1. Calculate based on L, U(L), S(L)
2. Take a prime number

## Rehashing

* Amortized analysis:
  1. Assume $O(1)$ operation to insert up to $M$ items: $O(M)$
  2. For the $(M+1)$-th item, create a new table of size 4M: $O(1)$.
  3. Rehash all $M$ items into the new table: $O(M)$
  4. Insert new item: $O(1)$