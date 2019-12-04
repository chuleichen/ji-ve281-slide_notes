# VE281 Slide10 Bloom Filter

* Pros: more space efficient, fast insert and find.
* Cons: 
  1. Can't store associated object (key, value)pair
  2. No deletion
  3. Small false positive probability (say x is inserted while actually not)



size `n` array, `|S|` elements, `k` hash functions

| Test\True | 0              | 1              |
| --------- | -------------- | -------------- |
| 0         | True negative  | False Negative |
| 1         | False Positive | True Positive  |

Precision: $\frac{TP}{TP+FP}$

Recall: $\frac{TP}{TP+FN}$

F-measure: $\frac{2 \times precision \times recall}{precision + recall}$

Accuracy: $\frac{TP+TN}{TP+TN+FP+FN}$



Error rate of bloom filter, $n = b|S|$, $k$ hash functions

j's slot $Pr(A[j]=0) = (1-1/n)^{k|S|} = e^{-\frac{k|S|}{n}} = e^{-\frac{k}{b}}$

​		$lim_{n \rightarrow \infin}(1-1/n)^{-n} = e$

​		$  Pr(h_i(x) \not= j) = (1-e^{-k/b}) $, $ Pr(all) = (1-e^{-k/b})^k = \epsilon $

$\min(1-e^{-k/b})^k$, let $x = e^{-k/b}$, and $x \in (0, 1)$

​		Set $f(x) = \ln \epsilon = -n \ln x\ln (1-x) \rightarrow min f(x), x \in (0, 1)$

​		$f'(x) = -b \cdot \frac{\ln(1-x)}{x} + (-b)\cdot (-1) \cdot \frac{\ln x}{1-x} = 0 \Rightarrow x = \frac{1}{2}$

let $g(x) = -\ln (1-x)\cdot(1-x)+\ln x \cdot x$

​		$g(x) = 1 +\ln (1-x) + 1 + \ln x = 2 + \ln x + \ln (1-x)$

​				$x \in (0, \frac{1}{2}), \ln x \cdot(1-x) \rightarrow (-\infin, \ln \frac{1}{4})$

​				$ x \in (\frac{1}{2}, 1), \ln x \cdot(1-x) \rightarrow (\ln \frac{1}{4}, -\infin) $

​				$g'(x) \ neg \rightarrow pos \rightarrow neg$ 

​				$f(x)$ only has one root

​		$\epsilon = (1- e^{-k/b})^k, x = e^{-k/b}$ will get minimum with $x = \frac{1}{2}$ 

​		$\Rightarrow k = b \cdot \ln 2$ 