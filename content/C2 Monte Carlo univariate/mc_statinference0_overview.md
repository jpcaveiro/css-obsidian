
# Overview of inference cases using MC

Monte Carlo method requires:
* a population $X$ (explicit distribution of $X$ can be **known** or **unknown**)
* an estimator $T$ for a parameter $\theta$ of that population (the explicit distribution of $T$ can be **known** or **unknown**)
* one has a single sample or $N$ samples (one can have a single sample of size $n$ or $N$ samples of size $n$)

We have this cases:

1. Explicit distribution of $X$ is unknown:
	* (this is, also, the theme for [[_Chapter 3_start_|Chapter 3 - Bootstrap and Jackknife methods]]).
	
2. Distribution of $X$ is known:
	* distribution of $T$ is unknown, sample size $n$ is small.
	* distribution of $T$ is unknown, sample size $n$ is large.
	* distribution of $T$ is known, sample size $n$ is small.
	* distribution of $T$ is known, sample size $n$ is large.

The Monte Carlo recipe is:
1. Generate $N$ samples $X_1^{(j)},\dots,X_n^{(j)} \sim F_X$, for $j=1,\dots,N$.
2. Compute $T_j = T(X_1^{(j)},\dots,X_n^{(j)})$.
3. Use the empirical distribution of $T_1,\dots,T_N$ in place of the distribution of $T$:
	* $\hat E[T]=\bar T$ (mean of estimates)
	* $\widehat{\text{bias}}=\bar T-\theta$ (bias of the statistic $T$, in PT is "viés") 
	* $\widehat{\text{Var}}(T)=s_T^2$ (variance of the statistic $T$)
	* $\widehat{\text{MSE}}=\frac1m\sum_j (T_j-\theta)^2$ (mean square error, in PT is "erro quadrático médio") 
	* $\widehat{\chi_{p,T}}$  by estimating $P(T \leq \widehat{\chi_{p,T}})=p$ (quantiles).

Consider the survey of **applications of Monte Carlo method**:

| Distribution of $T$ | $n$ small                                                                                                                                                                                                                                                | $n$ large                                                                                                                                                                                                    |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Unknown**         | **MC is the main tool.** No exact result exists, and asymptotic results are unreliable. Apply the MC algorithm to get the bias, variance, MSE and quantiles of $T$. [[_Chapter 3_start_\|In the next chapter: Bootstrap or jackknife methods also help]] | **Use asymptotics first** (see [[LLM C2 common asymptotic tests]]). Use MC to estimate a parameter when it has no closed form, and check, for example, that a normal approximation is adequate for this $n$. |
| **Known**           | **MC is not needed.** Use the exact distribution. **Use MC only to validate theory or code**, for example by comparing the histogram of the $T_j$ with the exact density.                                                                                | **MC is not needed.** Use the exact or asymptotic distribution. **Use MC only for validation, or to compare the exact and asymptotic distributions.**                                                        |
- MC precision depends on $N$, not $n$: $\text{se}(\bar T)=s_T/\sqrt N$.
