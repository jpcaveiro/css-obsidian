
Note about word "Omnibus":
* "Omnibus" = a single statistic that aggregates evidence against the null across **all possible** alternatives. 
* A skewness-only test is the opposite — a **directional** or **component** test — which is more powerful for _its_ specific alternative but blind to everything else.


Normality tests based on **asymmetry** (skewness) — such as D'Agostino's skewness test, Geary's test, or the skewness component of the Jarque-Bera procedure — assess departure from normality by checking whether the third standardized moment $\gamma_1 = E[(X-\mu)^3]/\sigma^3$ differs from zero (the normal value). 

Here are the main trade-offs.

## Pros

- **Intuitive interpretation.** Skewness measures directional asymmetry, which is easy to communicate: a positive/negative value signals a longer right/left tail. This makes the test transparent compared to black-box omnibus statistics.
- **Computationally simple.** It reduces to a single moment-based statistic (or a ratio involving the mean absolute deviation, as in Geary's test), so it is cheap to compute and easy to implement from scratch.
- **Good power against skewed alternatives.** When the true distribution is asymmetric (lognormal, exponential, gamma, etc.), a skewness-based test is specifically targeted at that deviation and can outperform general-purpose tests.
- **Complements kurtosis tests.** Combined with a kurtosis check (as in the Jarque-Bera test), it gives a moment-based decomposition of non-normality into "shape" components, which is diagnostically useful.

## Cons

- **Only tests one dimension of normality.** A distribution can be perfectly symmetric ($\gamma_1 = 0$) yet clearly non-normal — e.g., heavy/light tails (leptokurtic or platykurtic), bimodal, or uniform. The skewness test has essentially **no power against symmetric non-normal alternatives**.
- **High variance of the sample skewness estimator.** The third moment is sensitive to tail observations, so $\hat{\gamma}_1$ is unstable in small samples. This inflates the test's variance, distorts the nominal significance level, and weakens power relative to tests that use more of the sample information.
- **Suboptimal compared to omnibus tests.** For general alternatives, tests that exploit the full empirical distribution — **Shapiro-Wilk, Anderson-Darling, Cramér-von Mises** — typically have higher overall power because they compare the data to the normal reference more comprehensively.
- **Sensitive to outliers.** Because the third power weights extreme observations heavily, a few outliers can trigger rejection even when the bulk of the data is normal, lowering specificity.
- **Large-sample sensitivity (shared caveat).** Like all normality tests, with very large $n$ it rejects for negligible deviations that are practically irrelevant, while with small $n$ it lacks power to detect real departures.

## Bottom line

A skewness-based normality test is a **focused diagnostic**, not a comprehensive normality check. It is most useful when you specifically care about asymmetry or want to decompose non-normality into interpretable components. For a general "is this sample normal?" decision, an omnibus test (Shapiro-Wilk or Anderson-Darling) is usually preferable, often supplemented by a Q-Q plot rather than relying on a single moment.


Reference:
* https://www.perplexity.ai/computer/tasks/c1357f96-e473-47dc-90d5-957309ca04ca