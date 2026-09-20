* https://www.perplexity.ai/computer/tasks/c1357f96-e473-47dc-90d5-957309ca04ca

Recall:

* $E[(X - \mu)^3]$ is the **third central moment** of the random variable X, usually denoted $\mu_3$​.
* $\sigma^3$ is the population standard deviation to cube instead of square like variance $\sigma^2$ 
* The third standardized moment is :
  $$\gamma_1 = \frac{E[(X-\mu)^3]}{\sigma^3}$$
* Note : the third moment $E[X^3]$ is not $\sigma^3$.



The **empirical asymmetry coefficient** (in Portuguese, _coeficiente de assimetria empírico_) is the sample version of skewness — a dimensionless number summarizing how asymmetric an observed dataset is. "Empirical" simply means it is computed from the sample rather than being a theoretical population parameter.

## The standard definition (moment-based)

Given a sample $x_1, \dots, x_n$, the empirical skewness coefficient is the third standardized central moment estimated from the data:

$$
g_1 \;=\; \frac{m_3}{m_2^{3/2}} \;=\; \frac{\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^3}{\left[\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2\right]^{3/2}}
$$

where $m_2$ and $m_3$ are the second and third empirical central moments, and $\bar{x}$ is the sample mean.

A **bias-corrected** estimator (Fisher's $G_1$) adjusts the denominator for small samples and is the version most software reports.

## Interpretation

- $g_1 \approx 0$: roughly symmetric distribution.
- $g_1 > 0$: **positive/right skew** — right tail longer, mass concentrated on the left.
- $g_1 < 0$: **negative/left skew** — left tail longer, mass concentrated on the right.

For a perfectly normal population, $\gamma_1 = 0$, which is why testing whether $g_1$ differs from zero is the basis of the skewness-based normality test discussed earlier.

## Alternative "asymmetry coefficients"

The term is sometimes used more loosely for other measures of skewness that are also computable from data:

- **Pearson's first coefficient:** $(\bar{x} - \text{mode})/s$
- **Pearson's second coefficient:** $3(\bar{x} - \text{median})/s$
- **Bowley / quartile coefficient:** $\dfrac{Q_3 + Q_1 - 2\,Q_2}{Q_3 - Q_1}$

These are more robust to outliers but less efficient statistically, since they use only a few summary points (mode, median, quartiles) instead of the full moment structure.

## In short

The empirical asymmetry coefficient is the **sample skewness** $g_1$: a standardized third moment that quantifies, on a scale centered at zero, how much an observed distribution leans to one side. It is the empirical counterpart of the population skewness $\gamma_1$ and the statistic behind asymmetry-based normality tests.