# VE281 Slide03 Comparison Sort

[TOC]

## Sorting basics

* Ascending order (default) & Descending order
* Comparison sort & Non-comparison sort (put into predefined "bins")
* In place: requires $O(1)$ additional memory
* Stability: whether the algorithm maintains the relative order of records with equal keys.

#### $\Omega$ for best case, $O$ for worst and average case, $\Theta$ when best case = worst case

###  Insertion Sort

* Insert A[i] into the appropriate location in the sorted array.

* Time complexity:  $O(N^2)$

* In place and stable

* Average Cases Analysis: 

  $$ \frac{i}{i+1}+\sum_{j=1}^i\frac{i-j+1}{i+1} = \frac{i}{i+1} + \sum_{j=1}^i \frac{j}{i+1} $$
  $$ T(n) = O(\frac{n^2}{4}) = O(n^2) $$

### Selection Sort

* For i = 0 to N - 2, find the smallest item in the array A[i], ..., A[N - 1] and swap that item with A[i].
* Requires linear scan.

### Bubble Sort

* Compare two element and swap.
* Time complexity: $O(N^2)$
* In place and stable

## Merge Sort

1. Split into two (roughly) equal subarrays.

2. Merge sort each subarray recursively.

   ```c++
   void mergesort(int *a, int left, int right) { 
   	if (left >= right) return; 
   	int mid = (left+right)/2; 
   	mergesort(a, left, mid);                    //T(N/2)
   	mergesort(a, mid+1, right);                 //T(N/2)
   	merge(a, left, mid, right);                 //O(N)
   }
   ```

   * Time complexity: $T(N) = 2T(N/2) + O(N)$ (recursively defined)

3. Merge two sorted subarrays into a sorted array.

   * Compare the smallest element in A and B, move the smaller one to C.
   * Repeat until one array becomes empty.
   * Append the other array to the end of C.
   * Time complexity: $O(size A ＋ size B)$

* Not in-place

* Stable if `merge()` maintains the relative order of equal keys.
* Use the divide-and-conquer approach.

### Master Method

* Recurrence: $T(n) \leq aT(\frac{n}{b}) + O(n^d), a=1, b=2, d=0$
  * Base case: $T(n) \leq constant$ for all sufficiently small $n$.
  * $a$ = number of recursive calls (integer $\geq$ 1)
  * $b$ = input size shrinkage factor (integer > 1)
  * $O(n^d)$: the runtime of merging solutions. $d$ is real value $\geq$ 0.
  * $a$, $b$, $d$ are independent of $n$.
* Claim: $T(n) = O(n \log n)$

### Master Theorem 

* $ T(n) = aT(\frac{n}{b}) + O(n^d), a \geq 1, b>1, d \geq 0 $

<img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide03%20Comparison%20Sort.assets%5C%E6%8D%95%E8%8E%B7.PNG" alt="捕获" style="zoom:50%;" />
$$
\begin{aligned}
	Total =& \sum_{j=1}^ka^{j-1}\cdot O(\frac{n}{b^{j-1}})^d \\
	=& \sum_{j=0}^{k-1}a^j\cdot O(\frac{n}{b^j})^d \\
	=& O(n^d)\cdot \sum_{j=0}^{k-1}O(\frac{a}{b^d})^j
\end{aligned}
$$


1. $\frac{a}{b^d} = 1 \Rightarrow d= \log _b a$
   $ Total = O(n^d)\cdot \sum_{j=0}^{k-1}O(1)^j = O(n^d)\cdot \sum_{j=0}^{\log_bn} \cdot 1 = O(n^d \cdot \log_bn) = O(n^d\log n) $
   * **Base change formula**: $\log_b n = \frac{\log_2n}{\log_2b} = \frac{1}{\log_2b}\cdot \log_2n = c \cdot \log n$
2. $ \frac{a}{b^d} < 1 \Rightarrow d > \log_b a $
   $ q=\frac{a}{b^q}<1, a_1 = 1 $
   $ Total = O(n^d) \cdot \sum_{j=0}^{k-1}O(\frac{a}{b^d})^j \leq O(n^d) \cdot \frac{1}{1-\frac{a}{b^d}} = O(n^d) $
   * $ S_n = \sum a_1q^{n-1} = a_1 \cdot \frac{1-q^n}{1-q} \leq \frac{a_1}{1-q} $
3. $ \frac{a}{b^d}>1 \Rightarrow d < \log_ba $
   $q' = \frac{b^d}{a}, a' = (\frac{a}{b^d})^{k-1}$
   $ Total = O(n^d) \cdot \sum_{j=1}^{k-1}(\frac{a}{b^d})^j \leq O(n^d) \cdot \frac{(\frac{a}{b^d})^{k-1}}{1-\frac{b^d}{a}} = O(n^d) \cdot \frac{a^{\log_bn}}{b^{d \cdot \log_bn}} = O(n^d) \cdot \frac{n^{\log_ba}}{n^d} = O(n^{\log_ba}) $
   * $ a^{\log_bn} = a^{\log_an \cdot \log_ba} = n^{\log_ba} $

<img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide03%20Comparison%20Sort.assets%5C%E6%8D%95%E8%8E%B7-1568798831181.PNG" alt="捕获-1568798831181" style="zoom:50%;" />

## Quick Sort

1. Choose an array element as `pivot`.

2. Put all elements < pivot to the left of it.

3. Put all elements $\geq$ pivot to the right of it.

4. Move pivot to its correct place in the array.

5. Sort left and right subarrays recursively.

   ```c++
   void quicksort(int *a, int left, int right) { 
   	int pivotat;                                // index of the pivot 
   	if(left >= right) return; 
   	pivotat = partition(a, left, right);        // O(N)
   	quicksort(a, left, pivotat-1);              // T(Left size)
   	quicksort(a, pivotat+1, right);             // T(Right size)
   }
   ```

   

* Randomly pick the pivot: average running time is $O(n \log n)$.

* In-place partitioning the array:

  1. Once pivot is chosen, swap pivot to the beginning of the array.
  2. Start counters i=1 and j=N-1.
  3. Increment i until we find element A[i]>=pivot. (A[i] is the leftmost item ≥ pivot.)
  4. Decrement j until we find element A[j]<pivot. (A[j] is the rightmost item < pivot.)
  5. If i<j, swap A[i] with A[j]. Go back to step 3.
     <img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide03%20Comparison%20Sort.assets%5C%E6%8D%95%E8%8E%B72.PNG" alt="捕获2" style="zoom:50%;" />
  6. Otherwise, swap the first element (pivot) with A[j].
     <img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide03%20Comparison%20Sort.assets%5C%E6%8D%95%E8%8E%B72-1568798923658.PNG" alt="捕获2-1568798923658" style="zoom:50%;" />

  * Time complexity: $O(N)$.

* $T(N) = T(LeftSz) + T(RightSz) + O(N)$
  $LeftSz + RightSz = N - 1$
  Worst case:
  $$
  \begin{aligned}
  	T(N) &= T(N-1)+T(0)+O(N) \\
  	& \leq T(N-1) + T(0) + dN \\
  	& \leq T(N-2) + 2T(0) + d(N-1) + dN \\
  	& \ \ \ \ \ \ \cdots \\
  	& \leq T(0) + NT(0) +d+2d+\cdot +d(N-1) + dN \\
  	& = O(N^2)
  \end{aligned}
  $$
  Best case:

  $$ T(N) = T((N-1)/2) + T((N-1)/2) + O(N) = O(N \log N) $$

* Weakly in-place

* Not stable

## Comparison Sorts

### Worst case time complexity

* Theorem: A sorting algorithm that is based on pairwise comparisons must use $\Omega(N \log N)$ operations to sort in the worst case.

<img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide03%20Comparison%20Sort.assets%5C%E6%8D%95%E8%8E%B7-1568972120277.PNG" alt="捕获-1568972120277" style="zoom:50%;" />

* The depth of the tree: the worst-case time complexity of the algorithm.
* Every permutation must appear as the label of a leaf. ($n!$ leaves)
* $\log (n!) \approx \log(\sqrt{\pi(2n+1/3)}\cdot n^n \cdot e^{-n}) = \Omega(n \log n)$ (Stirling's formula)
  

## Summary

* Theorem: A sorting algorithm that is based on pairwise comparisons must use $\Omega(N \log N)$ operations to sort in the worst case.

| Algorithm      | Best Case          | Average Case       | Worst Case        | Stable | In-Place, S(n)              |
| -------------- | ------------------ | ------------------ | ----------------- | ------ | --------------------------- |
| Linear Search  | $\Omega(1)$        | $O(n)$             | $O(n)$            | -      | Yes, $O(1)$                 |
| Binary Search  | $\Omega(1)$        | $O(\log n)$        | $O(\log n)$       | -      | No, $O(\log n)$             |
| Selection Sort | $\Theta(n^2)$      | $\Theta(n^2)$      | $\Theta(n^2)$     | No     | Yes, $O(1)$                 |
| Bubble Sort    | $\Theta(n^2)$      | $\Theta(n^2)$      | $\Theta(n^2)$     | Yes    | Yes, $O(1)$                 |
| Insertion Sort | $\Omega(n)$        | $O(n^2)$           | $O(n^2)$          | Yes    | Yes, $O(1)$                 |
| Merge sort     | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $\Theta(n\log n)$ | Yes    | No, $O(\log n)$\Yes, $O(n)$ |
| Quick Sort     | $\Omega(n \log n)$ | $O(n \log n)$      | $O(n^2)$          | No     | Weakly (no), $O(\log n)$    |

1. Linear Search
   * Average case: $E[cost] = \sum_{i=0}^n Pr(i=x) \cdot cost(i) = \sum_{i=0}^n \frac{i}{n} = O(n)$
2. Merge Sort: $T(n) = 2T(\frac{n}{2}) +O(n)$
   Depth first search: one branch to the bottom and next branch.
3. Quick Sort: $ T(n) = T(n-1)+O(n) $



## Stack Usage

1. Web browser: first in, last out.
2. Parenthesis matching: one symbol stack and one number stack, o look-up table to check the priority. 
3. Hanoi tower
   <img src="C:%5CUsers%5CTP%5CDownloads%5CTypora%20Notes%5CVE281%5CSlide%5CVE281%20Slide03%20Comparison%20Sort.assets%5C%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20190925172232.png" alt="微信图片_20190925172232" style="zoom: 25%;" />