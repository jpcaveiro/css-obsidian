# Point and Interval Estimation

![[Pasted image 20260717104924.png]]

# Next: a change in notation

In what comes, MC will generate $N$ sets of samples of size $n$:

* $X_1^{(1)}, X_2^{(2)}, \ldots,X_n^{(1)}$ (first sample of size $n$)
* ... and so on ...
* $X_1^{(N)}, X_2^{(N)}, \ldots,X_n^{(N)}$ (last sample of size $n$).

and for each sample a estimation is done with some statistics $T$:
* $T^{(1)} = T(\text{sample 1})$
* and so on
* $T^{(N)} = T(\text{sample N})$

So, there are two sample sizes:
- $n$ is the number of observations in each simulated sample;
- $N$ is the number of simulation replications.

For example $n=20,\quad N=10\,000$ means that we generate 10,000 independent samples, each containing 20 observations. The estimator is calculated once for each sample.

Each sample of size $n$ will provide an estimation for a parameter as explained in next sections.
# Point Estimate

[[recall a concept]]:
* [[unbiased estimator]]

![[Pasted image 20260717104935.png]]

[[Memory is Something We Do]]

Exercise 1. If $T$ is the sample mean, check that  $\hat \mu$ is the same as
$$
\frac{1}{N n} \sum_{i=1}^N \sum_{j=1}^n X_j^{(i)}
$$
Exercise 2. Why Monte Carlo method rely on several samples and estimates $T^{(1)}, T^{(2)}, \ldots, T^{(N)}$?

# Confidence interval

[[recall a concept]]:
* [[Slutsky theorem]]


![[Pasted image 20260717104945.png]]





