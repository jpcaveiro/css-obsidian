
# Worksheet 3: Monte Carlo Methods

* Based on Academic year 2025/26 "worksheet 2" (from Ex. 7).
* This file contains the exercises of year 2025/26 but only from Ex. 7 to Ex. 10, all about Bootstrap and Jackknife methods.

---

**Exercise 7**. The data in the file `"tabaco.txt"` come from a study on the relationship between tobacco and lung cancer. Twenty-five occupational groups were studied. The explanatory variable $x$ is the number of cigarettes smoked per day by male individuals in each occupational group. The response variable $y$ is the standardized mortality rate due to deaths from lung cancer.
**(a)** Plot the data and obtain the empirical correlation coefficient.
**(b)** Generate 1000 **bootstrap** samples of the data, obtain the corresponding correlation coefficient and compute an estimate of the standard error of the correlation coefficient.

**Exercise 8**. Consider the data on the duration of the eruptions of the *Old Faithful* geyser — available in the R library `MASS` as `faithful$eruptions`. The aim is to determine a confidence interval for the mean of the population underlying the data. Using the estimator $\bar{X}$, determine that confidence interval by the bootstrap resampling method.

**Exercise 9**. For a sample $X_1,\dots,X_n$ i.i.d. as $X$, consider the estimator $\hat\theta_n=\bar{X}$ of the mean of $X$. We then know that $se(\hat\theta_n)=\sqrt{\operatorname{Var}(X)/n}$. Show that
**(a)** $\hat\theta_{(j)}=\dfrac{n\bar{X}-X_j}{n-1}$;
**(b)** $\bar{\hat\theta}_{(\cdot)}=\bar{X}$;
**(c)** $\widehat{se}_{jack}(\hat\theta_n)=\sqrt{S_n^{2}/n}$, with $S_n^{2}=\dfrac{1}{n-1}\sum_{j=1}^{n}(X_j-\bar{X})^{2}$.

**Exercise 10**. Solve Exercise 7 (see [[_Chapter 2_worksheet_]] ) using the Jackknife resampling method to estimate the correlation and compute an estimate of its bias.
