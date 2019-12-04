# VE281 Slide05 Linear Time Selection

### The Selection Problem

* Output the $i$-th smallest element in the array $A$. (Assume the index start from 1) 

## Randomized Selection

```c++
Rselect(int A[], int n, int i) { 
    // find i-th smallest item of array A of size n 
    if(n == 1) return A[1]; 
    Choose pivot p from A uniformly at random; 
    Partition A using pivot p; 
    Let j be the index of p; 
    if(j == i) return p; 
    if(j > i) return Rselect(1st part of A, j-1, i); 
    else return Rselect(2nd part of A, n-j, i-j);
}
```

* Average runtime of Rselect: $O(n)$

* Rselect is in phase $j$ if the current array size is between $(3/4)^{j+1}n$ and $(3/4)^jn$

* Average Runtime Analysis

  Good pivot: choose a pivot so that the left subarray's size is $am$, where $a \in [\frac{1}{4}, \frac{3}{4}]$ and $m$ is the old length. The probability of a good pivot is 0.5 .
  $X_j$ denote the number of recursive calls in the phase $j$: ($[(3/4)^{b+1}, (3/4)^b]n \leq (3/4)^b\cdot n$), the possibility from phase $i$ to phase $i+1$.
  When for $X_k$, $[(3/4)^{k+1}, (3/4)^k]n \leq 1$, we have $k = \log_{3/4}n$
  $runtime = \sum_{a=0}^{no \ interation}c \cdot l_a = \sum_{b=0}^{\log_{3/4}n}c \cdot X_b \cdot (3/4)^b \cdot n$
  $E[runtime] = E[\sum_{b=0}^{\log_{3/4}n}c \cdot X_b \cdot (3/4)^b \cdot n] = \sum_{b=0}^{\log_{3/4}n} c \cdot (3/4)^b \cdot n \cdot E[X_b]$
  $Pr(X_b=X) = (1-p)^{x-1} \cdot p$

  $E[X_j] \leq Expected\ number\ of\ times\ need\ to\ get\ a\ good\ pivot$
  $E[X_b] = p \cdot 1 + (1-p)\cdot(1+E[X_b]) \Rightarrow E[X_b]= 1/p = 2$

  $E[runtime]\leq 2cn\frac{1}{1-3/4} = 8cn = O(n)$ 

## Deterministic Selection Algorithm

```c++
Dselect(int A[], int n, int i) { 
    // find i-th smallest item of array A of size n 
    if(n == 1) return A[1]; 
    Break A into groups of 5, sort each group;           //Theta(n)
    C = n/5 medians; 									 //Theta(n)
    p = Dselect(C, n/5, n/10);                           // T(n/5)
    Partition A using pivot p;                           // Theta(n)
    Let j be the index of p; 
    if(j == i) return p; 
    if(j > i) return Dselect(1st part of A, j-1, i); 
    else return Dselect(2nd part of A, n-j, i-j);
}
```

* Choose a pivot:
  1. Break $A$ into $n/5$ groups of size 5 each. (shrink the array into a n/5 size)
  2. Sort each group.
  3. Copy $n/5$ medians into new array C.
  4. Recursively compute median of C.
  5. Return the median of C as pivot.
* Not in-place