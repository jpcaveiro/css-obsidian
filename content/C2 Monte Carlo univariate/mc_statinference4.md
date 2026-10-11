# statistical tests

[[Background reading]]: 
* [[LLM C2 statistical tests tiny summary]]
* [[LLM C2 common asymptotic tests]]

Consider the problem and the read the [[mc_statinference0_overview|survey of MC uses in inference]]:
![[Pasted image 20260923101932.png]]


[[to do]] - improve documentation based on [[LLM C2 Worksheet 2 Exercise 6]] and 
* importante: https://www.perplexity.ai/search/2e25859f-0e3c-4ea9-9cfa-2129693921ce  
* http://nguyen.hong.hai.free.fr/EBOOKS/SCIENCE%20AND%20ENGINEERING/MATHEMATIQUE/MATLAB/Computational.Statistics.Handbook.With.MATLAB/Chapter%206.pdf
* 


To give or not to give $\alpha$ in a statistical test.


![[Pasted image 20260717114152.png]]





![[Pasted image 20260717114210.png]]

![[Pasted image 20260717114222.png]]

# p-value

Estimating p-values is one of the standard uses of Monte Carlo methods.

A p-value is a probability under $H_0$:

$$
p = P_{H_0}(T \ge t_{obs}).
$$

When the null distribution of the test statistic $T$ is unknown or hard to work out, you simulate it:

1. Compute $t_{obs}$ from the observed data.
2. Generate $M$ datasets under $H_0$, each the same size as your real data.
3. Compute $T_1, \dots, T_M$, one from each simulated dataset.
4. Estimate the p-value as

$$
\hat p = \frac{1 + \#\{T_j \ge t_{obs}\}}{M + 1}.
$$

The "+1" counts the observed sample as one of the draws from $H_0$. This means $\hat p$ is never exactly 0, and the test keeps its nominal size.

## Small R example

```r
x <- c(2.1, 3.4, 1.9, 4.2, 3.8, 2.7)   # H0: X ~ Exp(rate = 1/2), mean 2
t_obs <- mean(x)
M <- 9999
t_sim <- replicate(M, mean(rexp(length(x), rate = 1/2)))
p_hat <- (1 + sum(t_sim >= t_obs)) / (M + 1)
```
Useful notes:

- **Precision:** $\hat p$ is a binomial proportion, so its Monte Carlo standard error is about $\sqrt{p(1-p)/M}$. A larger $M$ gives a more precise estimate.
- **Related methods:** Permutation tests and parametric bootstrap tests work the same way. The only difference is how you generate data under $H_0$: by permuting labels in one case, and by sampling from a fitted model in the other. [[_Chapter 3_start_|Chapter 3]] covers these. 



