notation:
* $\theta$ is a parameter (like $\mu$ in a normal distribution)
* $\hat \theta$ is an estimator (like $\bar X$ as an estimator for $\mu$)
* $E[\hat \theta]$ can be equal to $\theta$ (a centered estimator like $E[\bar X] = \mu$, or unbiased estimator) but $E[\hat \theta]$ can be different from $\theta$ (an estimator with bias)

[[definition]] of mean square error:
$$
\text{MSE}(\hat{\theta}) := E\left[\left(\hat{\theta} - \theta\right)^2\right]
$$
Considering that the **variance of the estimator** is
$$\text{Var}(\hat \theta) = E\left[ (\hat\theta - E[\hat \theta])^2 \right]$$
and **bias of the estimator** is 
$$\text{bias}(\hat\theta) = E[\hat\theta] - \theta$$then, [after same algebra](https://en.wikipedia.org/wiki/Mean_squared_error), **mean square error** is divided into its two components:
$$\text{MSE}(\hat \theta) = \text{Var}(\hat \theta) + \text{bias}(\hat \theta)^2$$
If estimator $\hat \theta$ is [[unbiased estimator|unbiased]], i.e. $E[\hat \theta]=\theta$, then 
$$\text{MSE}(\hat \theta) = \text{Var}(\hat \theta)$$

Notes:
* This definitions assumes that true $\theta$ is known and that $E[\hat \theta]$ is known. In this case, this measures are usefull to evaluate a theory using, for example, Monte Carlo simulations.
* If true $\theta$ is not known, one can use [[c3_03jackknife|Jacknnife]] method explained in [[_Chapter 3_start_|Chapter 3]] to estimate bias.
* To estimate $\text{Var}(\hat \theta)$ without know $E[\hat \theta]$, one can use sample variance (using sample mean $\bar {\hat \theta}$ for $E[\hat \theta]$).
* 