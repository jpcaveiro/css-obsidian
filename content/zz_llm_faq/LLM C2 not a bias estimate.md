
# Why a single Monte Carlo error is not a bias estimate

The key distinction is that **bias describes an estimator’s average behaviour, not the error of one observed estimate**. Thus, "without replicas, bias estimation does not make sense” is better phrased as “one run does not separate systematic bias from random error".[sites.pitt](https://sites.pitt.edu/~jch61/PS2740/Readings/Hopkins_etal.pdf)

## One error versus average error

Let $T_n=T(X_1,\ldots,X_n)$ estimate $\theta$. Its bias is defined over hypothetical repetitions of the entire sample:

$$
b_n=\mathbb E[T_n]-\theta.
$$

Monte Carlo bias estimation approximates this expectation by averaging estimates from repeated simulated samples.[sites.pitt](https://sites.pitt.edu/~jch61/PS2740/Readings/Hopkins_etal.pdf)

For one sample, the observed discrepancy decomposes as

$$
\underbrace{T_n-\theta}_{\text{realized error}}
=
\underbrace{\mathbb E[T_n]-\theta}_{\text{bias}}
+
\underbrace{T_n-\mathbb E[T_n]}_{\text{random fluctuation}}.
$$

Consequently, observing $T_n-\theta=0.2$ does not tell you whether the procedure systematically overestimates, or this particular sample happened to give a high estimate. Even an unbiased estimator generally produces estimates different from the truth.[sites.pitt](https://sites.pitt.edu/~jch61/PS2740/Readings/Hopkins_etal.pdf)

With $N$ independent replicas of the whole estimation procedure, the usual estimate is

$$
\widehat b_n
=
\frac1N\sum_{r=1}^{N}T_n^{(r)}-\theta,
\qquad
\widehat{\operatorname{SE}}(\widehat b_n)
=
\frac{s_T}{\sqrt N}.
$$

Replication averages out random fluctuations, and the standard error quantifies the remaining simulation uncertainty.[pmc.ncbi.nlm.nih](https://pmc.ncbi.nlm.nih.gov/articles/PMC3337209/)

## For ordinary Monte Carlo integration, bias is already zero

In your notes’ “integration goal with no replicas” setting,

$$
\theta=\mathbb E[g(X)],
\qquad
\widehat\theta_n=\frac1n\sum_{i=1}^{n}g(X_i).
$$

Assuming integrability and correct sampling from the target distribution, linearity of expectation gives

$$
\mathbb E[\widehat\theta_n]
=\frac1n\sum_{i=1}^{n}\mathbb E[g(X_i)]
=\theta.
$$

So **the bias is exactly zero by construction**, without needing empirical replicas to establish it.[jpcaveiro.github](https://jpcaveiro.github.io/css-obsidian/C2-Monte-Carlo-univariate/mc_quality)

A nonzero $\widehat\theta_n-\theta$ is therefore a realized Monte Carlo error, not evidence of bias; for i.i.d. draws with finite variance, its typical scale can be estimated from that single run using $s_g/\sqrt n$.[jpcaveiro.github](https://jpcaveiro.github.io/css-obsidian/C2-Monte-Carlo-univariate/mc_quality)

## A small but important qualification

It is not mathematically meaningless to use $T_n-\theta$ as a one-replica bias estimate when $\theta$ is known:

$$
\mathbb E[T_n-\theta]=b_n,
\qquad
\operatorname{Var}(T_n-\theta)=\operatorname{Var}(T_n).
$$

But this algebra shows the limitation: it retains all the variability of a single estimate, so the observed discrepancy does not reveal how much is systematic and how much is chance.

The practical message is: **do not call the error of one estimate “the bias.”** Either establish bias analytically, as for the ordinary Monte Carlo average, or use replicated estimates to assess average error with quantified simulation uncertainty (course notes; Koehler, Brown and Haneuse).[pmc.ncbi.nlm.nih](https://pmc.ncbi.nlm.nih.gov/articles/PMC3337209/)[jpcaveiro.github](https://jpcaveiro.github.io/css-obsidian/C2-Monte-Carlo-univariate/mc_quality)