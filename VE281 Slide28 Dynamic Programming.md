# VE281 Slide28 Dynamic Programming

## Introduction

* Greedy: build up a solution incrementally, myopically optimizing some local criterion.
* Divide-and-conquer: break up a problem into sub-problems, solve each sub-problem independently, and combine solution to sub-problems to form solution to original problem.
* **Dynamic programming**: break up a problem into a series of **overlapping** sub-problems, and build up solutions to larger and larger sub-problems.



## Basic Methodology

### Weighted Interval Scheduling

* Job $j$ starts at $s_j$, finish at $f_i$, and has weight or value $v_j$. Two jobs **compatible** if they don't overlap.

  * Goal: find maximum weight subset of mutually compatible jobs.
  * Greedy algorithm works if all weights are 1, but can fail if arbitrary weights are allowed.

* Notation: label jobs by finishing time: $f_1 \leq f_2 \leq \cdots \leq f_n$. 

  * $p(j) = $ largest index $i < j$ such that job $i$ is compatible with $j$.

  * $OPT(j) = $ value of optimal solution to the problem consisting of job request $1, 2, \cdots, j$.
    $$
    OPT(j) = \left\{  \begin{matrix} 0 & j = 0 \\ \max\{ v_j + OPT(p(j)), OPT(j-1)\} & otherwise \\ \end{matrix} \right.
    $$
    

      <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 202236.png" alt="批注 2019-12-04 202236" style="zoom:50%;" />

* Memoization version: store results of each sub-problem in a cache, look up as needed.

  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 204252.png" alt="批注 2019-12-04 204252" style="zoom:50%;" />

  * Time complexity: $O(n \log n)$
    * Sort by finish time: $O(n \log n)$.
    * Computing $p(\cdot)$: $O(n \log n)$ via sorting by start time.
    * M-Compute-Opt($j$): each invocation takes $O(1)$ time and either
      * returns an existing value $M[j]$.
      * fills in one new entry $M[j]$ and makes two recursive calls.
    * Progress measure $\Phi = $ number nonempty entries of $M[\cdot]$.
      * Increases $\Phi$ by $1 \Rightarrow $ at most $2n$ recursive calls.
    * Overall running time of M-Compute_Opt($n$) is $O(n)$.
  * Time complexity is $O(n)$ is jobs are pre-sorted by start and finish times.
  
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 210507.png" alt="批注 2019-12-04 210507" style="zoom:50%;" />
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 210538.png" alt="批注 2019-12-04 210538" style="zoom:50%;" />



### Segmented Least Squares

* Points lie roughly on a sequence of several line segments.
* Given $n$ points in the plane: $(x_1, y_1), \cdots, (x_n, y_n)$ with $x_1 < \cdots < x_n$, find a sequence of lines that minimizes:
  * the sum of the sums of the squared errors $E$ in each segment
  * the number of lines $L$
* Tradeoff function: $E+cL$, for some constant $c>0$.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 210935.png" alt="批注 2019-12-04 210935" style="zoom:50%;" />

* Notation:

  * $OPT(j) = $ minimum cost for points $p_1, p_{i+1}, \cdots, p_j$.
  * $e(i,j) = $ minimum sum of squares for points $p_i, p_{i+1}, \cdots, p_j$.

* Compute $OPT(j)$:

  * Last segment uses points $p_i, p_{i+1}, \cdots, p_j$ for some $i$.

  * $Cost = e(i,j)+c+OPT(i-1)$
    $$
    OPT(j) = \left\{ \begin{matrix} 0 & j = 0 \\ \min_{1\leq i\leq j}\{ e(i, j) + c + OPT(i-1) \} & otherwise \\ \end{matrix} \right.
    $$
    

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 211352.png" alt="批注 2019-12-04 211352" style="zoom:50%;" />

* Time complexity: $O(n^3)$
  * Can be improved to $O(n^2)$ by pre-computing.



### Knapsack Problem

* Given $n$ objects and a "knapsack". Item $i$ weighs $w_i>0$ kilograms and gas value $v_i>0$. Knapsack has capacity of $W$ kilograms.

* Goal: fill knapsack so as to maximize total value.

  * Greedy: repeatedly add item with maximum ratio $v_i/w_i$.

* Definition: $OPT(i) = $ max profits subsets of items $1, \cdots, i$ with **weight limit** $w$.

  * Case 1: OPT does not select item $i$.
    * OPT selects best of $\{ 1, 2, \cdots, i-1 \}$ using weight limit $w$.
  * Case 2: OPT selects item $i$.
    * new **weight limit** = $w-w_i$.
    * OPT selects best of using $\{ 1,2,\cdots,i-1 \}$ this new weight limit

  $$
  OPT(i,w) = \left\{  \begin{matrix} 0 & j=0 \\ OPT(i-1, w) & w_i>w \\ \max\{ OPT(i-1, w), v_i+OPT(i-1, w-w_i) \} & otherwise \\ \end{matrix} \right.
  $$

  

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide28 Dynamic Programming.assets\批注 2019-12-04 212702.png" alt="批注 2019-12-04 212702" style="zoom:50%;" />

* Time complexity: $\Theta(nW)$.