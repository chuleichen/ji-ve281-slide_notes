# VE281 Slide27 Greedy Algorithm

## Interval Scheduling

* Job $j$ starts at $s_j$ and finishes at $f_j$.
* Two jobs are compatible if they don't overlap.
* Goal: find maximum subset of mutually compatible jobs.

<img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide27 Greedy Algorithm.assets\批注 2019-12-04 182338.png" alt="批注 2019-12-04 182338" style="zoom:50%;" />

* Time complexity: $O(n \log n)$
  * After each iteration, set job $j^*$ that was added last to $A$.
  * Job $j$ is compatible with $A$ if $s_j \geq f_j^*$. 
* Greedy Interval Scheduling algorithm is optimal.
* The `depth` of a set of open intervals is the maximum number that contain any given time.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide27 Greedy Algorithm.assets\批注 2019-12-04 183930.png" alt="批注 2019-12-04 183930" style="zoom:50%;" />
  * Time complexity: $O(n \log n)$
  * Keep the classrooms in a priority queue.
* Greedy algorithm never schedules two incompatible lectures in the same classroom.



## Scheduling to Minimize Lateness

* Single resource processes one job at a time.
* Job $j$ requires $t_j$ units of processing time and is due at time $d_j$.
* If $j$ starts at time $s_j$, it finishes at time $f_j = s_j + t_j$.
* Lateness: $l_j = max\{ 0, f_i - d_i \}$.
* Goal: schedule all jobs to minimize the maximum lateness $L = \max l_j$.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide27 Greedy Algorithm.assets\批注 2019-12-04 185615.png" alt="批注 2019-12-04 185615" style="zoom:50%;" />
  * Time complexity: $O(n \log n)$.

* The greedy schedule has no idle time.
* Greedy schedule has no inversions.
  * Given a schedule $S$, an inversion is a pair of jobs $i$ and $j$ such that $i<j$ but $j$ schedule before $i$.
  * If a schedule (with no idle time) has an inversion, it has one with a pair of inverted jobs scheduled consecutively.
  * Swapping two consecutive, inverted jobs reduces the number of inversions by one and does not increase the max lateness.

## Coin Changing

* Given US currency denominations and devise a changing method using fewest number of coins.
* Cashier's algorithm: at each iteration, add coin of the largest value that dose not take us past the amount to be paid.
  <img src="C:\Users\AAAA\Downloads\Typora Notes\VE281\Slide\VE281 Slide27 Greedy Algorithm.assets\批注 2019-12-04 191639.png" alt="批注 2019-12-04 191639" style="zoom:50%;" />

* Greedy algorithm is optimal for US coinage.
* Not optimal for some example.
* Cannot find a solution for some example.

