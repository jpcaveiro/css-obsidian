The jackknife method is primarily used to **reduce bias** in statistical estimates and to **estimate variance (standard error)** when standard theoretical formulas are unavailable or unreliable.

### 📊 Core Uses of the Jackknife

*   **Bias Reduction**: Invented by Quenouille, it was originally designed to eliminate bias in an estimator by systematically leaving out one observation at a time and combining the results.
*   **Variance/Standard Error Estimation**: Tukey later popularized it as a general tool for estimating the variance of an estimator, which is especially useful for complex statistics like medians or ratios where simple formulas don't exist.
*   **Cross-Validation**: It serves as a "leave-one-out" validation technique, useful in **machine learning** and **survey statistics** to assess model stability.

It is considered a "rough-and-ready" tool (hence the name "jackknife") that predates the bootstrap, offering a computationally simpler way to handle tricky estimation problems.

References:
* https://www.cambridge.org/core/books/abs/introduction-to-computerintensive-methods-of-data-analysis-in-biology/jackknife/5B8BCAC4053816E2020CCA71B99E5704#1