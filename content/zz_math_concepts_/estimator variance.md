[[definition]]: Estimator variance is

$$\operatorname{Var}(\hat \theta) = E\left[ (\hat \theta - E[\hat \theta])^2 \right]$$

Notes:

* $E[\hat \theta]$ is not always equal to $\theta$ . See [[bias]].
* Combined with [[bias]], one gets [[mean square error]] via 
 
$$\text{MSE}(\hat \theta) = \text{Var}(\hat \theta) + \text{bias}(\hat \theta)^2$$

**efficiency**: if one has two estimators $\hat \theta_1$ and $\hat \theta_2$ and

$$\operatorname{var}(\hat \theta_1) < \operatorname{var}(\hat \theta_2)$$
then one say $\hat \theta_1$ is more efficient than  $\hat \theta_2$.


