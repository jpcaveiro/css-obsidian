
[[definition]] of mean square error:
$$
\text{MSE}(\hat{\theta}) := E\left[\left(\hat{\theta} - \theta\right)^2\right]
$$
It can be estimated by:
$$
\widehat{MSE}(\hat{\theta}) = \frac{1}{N} \sum_{i=1}^{N} \left(\hat{\theta}^{(i)} - \theta\right)^2
$$
 or
 $$\widehat{\text{MSE}}(\hat \theta) = \text{Var}(\hat \theta) + \text{bias}(\hat \theta)^2$$
 