# VE281 Slide04 Non-comparison Sort

## Counting Sort

* Not stable: Sort an array `A` of integers in the range` [0, k]`, where `k` is known
  1. Allocate an array `count [k+1]`.
  2. Scan array `A`. For `i=1` to `N`, increment `count[A[i]]`.
  3. Scan array `count`. For `i=0` to `k`, print `i` for `count[i]` times.
* Time complexity: $O(N + k)$
* In the range `[a, b]`: converting the range to `[0, b-a]`.
* Stable:
  1. Allocate an array `C[k+1]`.
  2. Scan array `A`. For `i=1` to `N`, increment `C[A[i]]`.
  3. For `i=1` to `k`, `C[i] = C[i-1]+C[i]`. (`C[i]` contains number of items less than or equal to `i`)
  4. For `i=N` down to `1`, put `A[i]` in new position `C[A[i]]` and decrement `C[A[i]]`.

## Bucket Sort

* Distribute elements by the keys and do a comparison sort inside a bucket.
* Average case time complexity: $O(N)$

## Radix Sort

* Sort integers by looking at one digit at a time, from least significant bit to most significant bit repeatedly doing stable bucket sort.
* For base-b numbers, need b buckets.
* Time complexity, $k$ is the maximum number of digits and N is the number of keys: $k\cdot O(N) = O(kN)$
* Can  be applied to sort keys that are built on positional notation and records with multiple keys.