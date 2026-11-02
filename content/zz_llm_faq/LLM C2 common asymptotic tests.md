
The Z test is just one of many tests whose level $\alpha$ holds only asymptotically. Any of them can be used for the exercise on your slide: simulate under $H_0$ with a small $n$ and estimate the real rejection rate $\hat\alpha = \frac{1}{m}\sum_{j=1}^m I(T^{(j)} \in R)$. Your vault doesn't have a note on this yet; the chi-square test only shows up in the C2 worksheet FAQ and in the "difference between two probabilities" FAQ.

## Common asymptotic tests

|Test|Statistic under $H_0$|Why it's only asymptotic|
|---|---|---|
|Z test for a mean when $\sigma$ is unknown or the data aren't normal|$\frac{\bar X-\mu_0}{S/\sqrt n} \xrightarrow{d} N(0,1)$|CLT plus Slutsky|
|Z test for a proportion|$\frac{\hat p-p_0}{\sqrt{p_0(1-p_0)/n}}$|CLT; poor when $np_0$ is small|
|t test on non-normal data|$t_{n-1}$|Exact only for normal data; robust only asymptotically|
|Pearson chi-square goodness of fit|$\sum \frac{(O_i-E_i)^2}{E_i} \to \chi^2_{k-1}$|Rule of thumb: $E_i \ge 5$|
|Chi-square test of independence (contingency tables)|$\chi^2_{(r-1)(c-1)}$|Same issue|
|Likelihood ratio test|$-2\log\Lambda \to \chi^2_q$|Wilks' theorem|
|Wald test|$\frac{(\hat\theta-\theta_0)^2}{\widehat{Var}(\hat\theta)} \to \chi^2_1$|Asymptotic normality of the MLE|
|Score (Rao) test|$\frac{U(\theta_0)^2}{I(\theta_0)} \to \chi^2_1$|Same|
|Chi-square test for the variance on non-normal data|$(n-1)S^2/\sigma_0^2 \sim \chi^2_{n-1}$|Very sensitive to kurtosis, and doesn't improve with $n$|
|Jarque–Bera normality test|$\to \chi^2_2$|Known to be badly undersized for small $n$|
|Kolmogorov–Smirnov with estimated parameters|Kolmogorov distribution|Wrong null distribution (this is why Lilliefors exists)|
|Large-sample Wilcoxon or Mann–Whitney|Normal approximation|Exact distribution is discrete|
|Kruskal–Wallis|$\to \chi^2_{k-1}$|Asymptotic|

## Sketch in R

Here is a sketch of the empirical size of the Z test for a proportion with small $n$, which has a classic erratic, discrete behaviour. I haven't run it.

```r
set.seed(1)
m <- 10000; n <- 15; p0 <- 0.2; alpha <- 0.05
rej <- replicate(m, {
  x <- rbinom(1, n, p0); ph <- x/n
  z <- (ph - p0)/sqrt(p0*(1-p0)/n)
  abs(z) > qnorm(1 - alpha/2)
})
alpha_hat <- mean(rej)
alpha_hat + c(-1,1)*1.96*sqrt(alpha_hat*(1-alpha_hat)/m)   # MC CI for the true level
```


The same approach works for the likelihood ratio, Wald and Pearson tests: replace the statistic and the critical value (for example $qchisq(1-alpha, df)$). Running it for several values of $n$ and plotting $\hat\alpha$ against $n$ shows how fast each test reaches its nominal level. You can also simulate under $H_1$ to estimate power.

