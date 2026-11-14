[[definition]]: Bias ("viés", in Portuguese) of an estimator $\hat \theta$ is this quantity
$$\text{bias}(\hat \theta) = E[\hat \theta] − \theta$$
If $\text{bias}(\hat\theta)=0$ then one say the estimator is **unbiased estimator**, otherwise one say it is **biased**.

Bias serves to **diagnose estimator quality**: it tells you whether an estimator systematically over- or under-shoots the target. 

For one sample, the observed discrepancy decomposes as

$$
\underbrace{\hat\theta_n-\theta}_{\text{realized error}}
=
\underbrace{\mathbb E[\hat\theta_n]-\theta}_{\text{bias}}
+
\underbrace{\hat\theta_n-\mathbb E[\hat\theta_n]}_{\text{random fluctuation}}
$$

Bias can be combined with [[estimator variance]], $\text{Var}(\hat \theta)$, via [[mean square error]] 
$$\text{MSE}(\hat \theta) = \text{Var}(\hat \theta) + \text{bias}(\hat \theta)^2$$
and mean square error that usually is the global quantity one wants to minimize.



Uses and methods:

- **Estimate it by Monte Carlo** (Chapter 2): simulate $N$ samples, compute $\hat \theta^{(i)}$ for each, average to approximate $E[\hat \theta]$, and subtract the true $\theta$ — a direct empirical check of whether an estimator is unbiased.
- **Estimate and correct it by resampling** (Chapter 3):
	- Bootstrap: $bias \approx (1/B) \sum \hat\theta^{(b)} − \hat\theta$, replacing the unknown $\theta$ with the original-sample estimate.
	- Jackknife: leave-one-out estimates $\hat \theta^{(j)}$ give both a bias estimate and the standard error √((n−1)/n · Σ(\hat \theta⁽ʲ⁾ − \hat \theta⁽·⁾)²) — the classic jackknife bias-corrected estimator is $\hat \theta$ − bias estimate,
- **Reason asymptotically** (Chapters 2 and 5): consistent estimators have bias vanishing as n → ∞, and Slutsky's theorem justifies plugging consistent estimators into known distributions — the basis for the t-statistic, and relevant when MLEs are only asymptotically unbiased.
- **Trade it off**: a biased estimator with small variance (e.g., shrinkage-type estimators) can beat an unbiased one in MSE terms — bias is a knob, not purely a defect.
