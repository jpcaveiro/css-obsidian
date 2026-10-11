## Tests with a critical region

1. State the hypotheses: null $H_0: \theta \in \Theta_0$ against alternative $H_1: \theta \in \Theta_1$ (one- or two-sided).
2. Choose the significance level $\alpha$ (e.g. 0.05). This is the maximum allowed probability of a Type I error.
3. Pick a test statistic $T = T(X_1,\dots,X_n)$ whose distribution under $H_0$ is known, exactly or asymptotically.
4. Typical examples: $Z=\frac{\bar X-\mu_0}{\sigma/\sqrt n}$, $T=\frac{\bar X-\mu_0}{S/\sqrt n}\sim t_{n-1}$, $\chi^2=\frac{(n-1)S^2}{\sigma_0^2}\sim\chi^2_{n-1}$.
5. Let $H_1$ decide the shape of the critical (rejection) region $C$, meaning the values of $T$ that are unlikely under $H_0$.
6. Right-tailed ($H_1:\theta>\theta_0$): $C=\{T > c_{1-\alpha}\}$.
7. Left-tailed ($H_1:\theta<\theta_0$): $C=\{T < c_{\alpha}\}$.
8. Two-tailed ($H_1:\theta\neq\theta_0$): $C=\{T<c_{\alpha/2}\}\cup\{T>c_{1-\alpha/2}\}$.
9. Get the critical values $c$ from the quantiles of the null distribution, so that $P_{H_0}(T\in C)=\alpha$, or $\le\alpha$ for discrete data.
10. Compute the observed statistic $t_{obs}$ from the sample.
11. Decision rule: if $t_{obs}\in C$, reject $H_0$. Otherwise, do not reject $H_0$. Not rejecting is not the same as accepting it.
12. The p-value gives the same decision: reject $H_0$ exactly when p-value $\le \alpha$.
13. Type I error: $\alpha=P(T\in C \mid H_0 \text{ true})$. Type II error: $\beta=P(T\notin C\mid H_1 \text{ true})$.
14. Power function: $\pi(\theta)=P_\theta(T\in C)$. A good test keeps $\pi\le\alpha$ on $\Theta_0$ and has high $\pi$ on $\Theta_1$.
15. Increasing $n$ lowers $\beta$ (raises power) while $\alpha$ stays the same. Lowering $\alpha$ shrinks $C$ and lowers power.
16. If the null distribution of $T$ is unknown, estimate $c$ by Monte Carlo: simulate $m$ samples under $H_0$, compute $T^{(j)}$ for each, and take the empirical quantile.
17. Monte Carlo estimate of the empirical Type I error: $\hat\alpha=\frac1m\sum_j I(T^{(j)}\in C)$, with standard error $\sqrt{\hat\alpha(1-\hat\alpha)/m}$.
18. Monte Carlo estimate of empirical power: simulate under a specific $\theta_1\in\Theta_1$ and compute $\hat\pi(\theta_1)=\frac1m\sum_j I(T^{(j)}\in C)$.
19. Check the assumptions (normality, independence, known or unknown variance) before trusting the critical values.
20. State the conclusion in context: "At level $\alpha$, the data do (or do not) provide evidence for $H_1$", and give $t_{obs}$, $C$ and the p-value.

Your vault has no note on this topic yet; the closest match for "critical region" was a Metropolis–Hastings note. So this summary follows standard course notation, including the Monte Carlo lines in the style of Chapter 2.