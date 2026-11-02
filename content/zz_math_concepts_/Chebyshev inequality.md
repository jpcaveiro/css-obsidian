

Let $X$ be a random variable with finite non-zero variance $\sigma^2$ (and thus finite expected value $\mu$.

Then for any real number $k > 0$
$$
P( | X − \mu | \ge k \sigma) \le \frac{1}{k^2}
$$
Or
$$
P( | X − \mu | \le k \sigma) ≤ 1-\frac{1}{k^2}
$$
Changing variable to $\epsilon = k\sigma$:

$$
P( | X − \mu | \le \epsilon) ≤ 1-\frac{1}{(\epsilon/\sigma)^2}
$$
or
$$
P( | X − \mu | \le \epsilon) ≤ 1-\frac{\sigma^2}{\epsilon^2}
$$

with $Var(X) = \sigma^2$.

Reference (online):
* https://en.wikipedia.org/wiki/Chebyshev%27s_inequality
