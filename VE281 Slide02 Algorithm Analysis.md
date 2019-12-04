# VE281 Slide02 Algorithm Analysis

## Measure Efficiency

1. Running size: S(n)
2. Running tine: T(n)
3. Best, worst, average cases
   * Best case: least number of steps required, corresponding to the ideal input.
   * Worst case: most number of steps required, corresponding to the most difficult input.
   * Average case: average number of steps required, given any input.
4. Average case or worst case is common

## Asymptotic Analysis

### Big-Oh

#### Definition: A non-negatively valued function, $T(n)$, is in the set $𝑂(𝑓(𝑛))$ if there exist two positive constants $𝑐$ and $n_0$ such that $T(n) \leq cf(n)$ for all $n \ge n_0$.

* $T(n)$ is in $O(f(n))$: $T(n) \in O(f(n))$ or $T(n) = O(f(n))$
* Big-oh notation indicates an upper bound.
* Look for the tightest upper bound.
* If $\lim_{n \rightarrow \infin} \frac{f(n)}{g(n)} = c < \infin$, then $f(n)$ is $O(g(n))$.

![](https://github.com/chuleichen/ji-ve281-slide_notes/tree/master/fig/fig1.png)

![](https://github.com/chuleichen/ji-ve281-slide_notes/tree/master/fig/fig2.PNG)

##### Rules:

1. If $f(n)$ = $O(g(n))$, then $cf(n) = O(g(n))$.
2. If $f_1(n) = O(g_1(n))$ and $f_2(n) = O(g_2(n))$, then $f_1(n) + f_2(n) = O(max\{g_1(n), g_2(n)\})$.
   For $n_{10}$, $f_1(n) \leq c_1g_1(n)$
   For $n_{20}$, $f_2(n) \leq c_2g_2(n)$
   For $max\{ n_{10}, n_{20} \}$, $f_1(n) + f_2(n) \leq c_1g_1(n) + c_2g_2(n) = 2max\{c_1, c_2\} \cdot max\{ g_1(n), g_2(n) \}$.
3. If $f_1(n) = O(g_1(n))$ and $f_2(n) = O(g_2(n))$, then $f_1(n) \cdot f_2(n) = O(g_1(n) \cdot g_2(n))$.
4. If $f(n) = O(g(n))$ and $g(n) = O(h(n))$, then $f(n) = O(h(n))$.

##### Examples:

1. $T(n) = a_k n^k + \cdots + a_1 n + a_0$ 
   $T(n) = O(n^k)$
   $n_0 = 1$
   $c = |a_k| + |a_{k-1}| + \cdots + |a_0|$
   $T(n) = a_kn^k + \cdots + a_0 \leq |a_k|n^k + \cdots + |a_0|n^k$
2. $T(n) = 2^{n+10} = 2^n \cdot 2^{10} = 1024 \cdot 2^n = O(2^n)$ 
3. For every integer $k \ge 1$, $log^kn = O(n)$
4. For every integer $k \ge 1$, $n^k = O(2^n)$

### Big-Omega

#### Definition: For $T(n)$ a non-negatively valued function, $T(n)$ is in the set $\Omega(g(n))$ if there exist two positive constants $c$ and $n_0$ such that $T(n) \ge cg(n)$ for all $n > n_0$.

* Big-omega gives a lower bound.
* Usually want the greatest lower bound.

### Big-Theta 

#### Definition: $T(n)$ is said to be in the set $\Theta(g(n))$ if it is in $O(g(n))$ and it is in $\Omega(g(n))$.

* There exist three positive constants $c_1$, $c_2$ and $n_0$ such that $c_1g(n) \le T(n) \le c_2g(n)$ for all $n > n_0$.

### Small-Oh

#### Definition: Let $f(n)$ and $g(n)$ be functions from the set of natural numbers to the set of nonnegative numbers. $f(n)$ is said to be $o(g(n))$, written $f(n) = o(g(n))$, if $\forall c, \exist n_0, \forall n \ge n_0, f(n) < cg(n)$.

### Small-Omega

#### Definition: Let $f(n)$ and $g(n)$ be functions from the set of natural numbers to the set of nonnegative numbers. $f(n)$ is said to be $\omega(g(n))$, written $f(n) = \omega(g(n))$, if $\forall c, \exist n_0, \forall n \ge n_0, f(n) > cg(n)$.

### Equivalence relation $\mathcal{R}$ and $\prec$

#### Definition: $f \mathcal{R} g$ if and only if $f(n) = \Theta(g(n))$.

#### Definition: $f \prec g$ iff $f(n) = o(g(n))$.

### Summary

Suppose $\lim_{n \rightarrow \infin} f(n) / g(n)$ exists.

* $\lim_{n \rightarrow \infin} \frac{f(n)}{g(n)} \not= \infin$ implies $f(n) = O(g(n))$.
* $\lim_{n \rightarrow \infin} \frac{f(n)}{g(n)} \not= 0$ implies $f(n) = \Omega(g(n))$.
* $\lim_{n \rightarrow \infin} \frac{f(n)}{g(n)} = c$ implies $f(n) = \Theta(g(n))$.
* $\lim_{n \rightarrow \infin} \frac{f(n)}{g(n)} = 0$ implies $f(n) = o(g(n))$.
* $\lim_{n \rightarrow \infin} \frac{f(n)}{g(n)} = \infin$ implies $f(n) = \omega(g(n))$.

## Time Complexity of Programs

* The complexity of atomic statement is $\Theta(1)$.
* The complexity of branch statement is that of the most expensive Boolean expression plus that of the most expensive branch. (if-else statement)
* This complexity of loops is related to the number of operations required in the loop.

##### Examples:

1. ```c++ 
   sum = 0;
   for (i = 1; i <= n; i++)
       sum += 1;
   ```

   The entire time complexity is $\Theta(n)$.

2. ```c++
   sum = 0;
   for (i = 1; i <= n; i++)
       for (j = 1; j <= i; j++)
           sum++;
   ```

   The time complexity is $T(n) = 1 + 2 + \cdots + n = n(n+1)/2 = \Theta(n^2)$.

3. ```c++
   sum = 0;
   for (i = 1; i <= n; i *= 2)
       for (j = 1; j <= n; j++)
           sum ++;
   ```

   The time complexity is $\Theta(n\log n)$