# statistical tests

[[Background reading]]: 
* [[LLM C2 statistical tests tiny summary]]
* [[LLM C2 common asymptotic tests]]

Consider the following problem

![[Pasted image 20260923101932.png]]

Recalling the [[mc_statinference0_overview|survey of MC uses in inference]], there are two uses of MC in statistical tests:

Use 1: when the T distribution allows the construction of analytical results to do statistical tests: one can use MC to verify, empirically, those results;

Use 2: otherwise, one can use MC to get an insight, empirically, of a statistical test.

In a statistical test, a researcher chooses a small probability value $\alpha$ defined has 

![[Pasted image 20261018091542.png]]

In "Use 1" above, a rejection region can be defined analytically. In "Use 2", MC is necessary to calculate the rejection region empirically (see [[mc_statinference2|quantile approximation]]).

In both cases, running a new set of simulations can be useful to estimate the level of significance $\alpha$ for $N$ large enough (see last formula):
![[Pasted image 20260717114222.png]]

Summarizing:

![[Pasted image 20260717114152.png]]



![[Pasted image 20260717114210.png]]

![[Pasted image 20260717114222.png]]


# p-value

Estimating p-values is one of the standard uses of Monte Carlo methods. A p-value is a probability under $H_0$:
$$
p = P_{H_0}(T \ge t_{obs}).
$$
When the null distribution of the test statistic $T$ is unknown or hard to work out, you simulate it:

1. Compute $t_{obs}$ from the observed data.
2. Generate $N$ datasets under $H_0$, each the same size as your real data.
3. Compute $T_1, \dots, T_N$, one from each simulated dataset.
4. Estimate the p-value as
$$
\hat p = \frac{1 + \#\{T_j \ge t_{obs}\}}{N + 1}.
$$

The "+1" counts the observed sample as one of the draws from $H_0$. This means $\hat p$ is never exactly 0, and the test keeps its nominal size.

## Small R example

```r
x <- c(2.1, 3.4, 1.9, 4.2, 3.8, 2.7)   # H0: X ~ Exp(rate = 1/2), mean 2
t_obs <- mean(x)
N <- 9999
t_sim <- replicate(N, mean(rexp(length(x), rate = 1/2)))
p_hat <- (1 + sum(t_sim >= t_obs)) / (N + 1)
```
Useful notes:

- **Precision:** $\hat p$ is a binomial proportion, so its Monte Carlo standard error is about $\sqrt{p(1-p)/M}$. A larger $M$ gives a more precise estimate.
- **Related methods:** Permutation tests and parametric bootstrap tests work the same way. The only difference is how you generate data under $H_0$: by permuting labels in one case, and by sampling from a fitted model in the other. [[_Chapter 3_start_|Chapter 3]] covers these. 


[[Memory is Something We Do]].

Solve [[_Chapter 2_worksheet_|Exercise 6]].


References:
* [Monte Carlo Methods for Inferential Statistics (© 2002 by Chapman & Hall/CRC)](http://nguyen.hong.hai.free.fr/EBOOKS/SCIENCE%20AND%20ENGINEERING/MATHEMATIQUE/MATLAB/Computational.Statistics.Handbook.With.MATLAB/Chapter%206.pdf)

