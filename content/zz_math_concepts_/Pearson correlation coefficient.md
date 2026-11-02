
It is a correlation coefficient that **measures linear correlation between two sets of data**. The usual notation is:

* $\rho(X,Y)$ is the population coefficient
* $R(X,Y)$ is the sample coefficient -- or small $r(X,Y)$.

The standard error of $R(X,Y)$ is given by
$$se(R) = \sqrt{\frac{(1-\rho^2)^2}{n}}$$

In R language,
* `cor(x,y)` function calculates $R$ for two numeric vectors.
* `sd()` function calculates the standard deviation of a sample (not the above formula).

References:
* https://en.wikipedia.org/wiki/Pearson_correlation_coefficient
* https://www.tandfonline.com/doi/abs/10.1080/01621459.1928.10502991


