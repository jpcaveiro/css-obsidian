The quantity
$$
\frac{1}{N}\sum_{i=1}^{N}g(X_i)-E[g(X)]
$$
is the **signed Monte Carlo error**, and
$$
\left|\frac{1}{N}\sum_{i=1}^{N}g(X_i)-E[g(X)]\right|
$$
is the **absolute Monte Carlo error**.

A note about **bias** (viés in portuguese). For independent samples,

$$
E\left[\frac{1}{N}\sum_{i=1}^N g(X_i)\right]=E[g(X)],
$$
 
so the Monte Carlo estimator is **unbiased** (sem viés in portuguese), even though its error in any particular simulation is generally nonzero.

The corresponding relative version is called the **relative Monte Carlo error**:

$$
\frac{\left|\frac{1}{N}\sum_{i=1}^{N}g(X_i)-E[g(X)]\right|}
{|E[g(X)]|},
$$

provided $E[g(X)]\neq 0$.