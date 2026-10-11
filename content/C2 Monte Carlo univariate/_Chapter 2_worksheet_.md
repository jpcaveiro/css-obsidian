
# Worksheet 2: Monte Carlo Methods

* This file contains the original exercises but **only** from Ex. 1 to Ex. 7, all about Monte Carlo simulation and inference and are based on "worksheet 2" from academic year 2025/26 .

---

**Exercise 1**. Obtain estimates of $p=P(X>2)$, with $X\sim C(0,1)$, i.e.,
   $$
   f(x)=\frac{1}{\pi(1+x^{2})},\qquad -\infty<x<\infty ,
   $$
using:
**(a)** the standard [[Cauchy distribution]];
**(b)** the [[Uniform distribution]] on $(0,2)$;
**(c)** it is known that $p=0.14758$. Compare the results obtained above and their variances.


**Exercise 2**. The aim is to compute the value of the integral
   $$
   I=\int_{0}^{\infty}\log(x)\,x^{5}e^{-3x}\,dx .
   $$
Using the Monte Carlo integration method, obtain estimates by simulating from:
**(a)** the distribution $X\sim Exp(3)$;
**(b)** the distribution $X\sim Ga(6,3)$;
**(c)** also use the replication method to estimate $I$ with $X\sim Ga(6,3)$;
**(d)** it is known that $I=0.1000009$. Compare the results obtained above with the exact value and with the estimate of the integral (and its error) in the case of the replication method.


**Exercise 3**. The aim is to estimate the integral
$$
   \int_{0}^{1}\frac{e^{-x}}{1+x^{2}}\,dx
$$
using the importance sampling technique. Consider the following candidate importance functions:
$$
   f_1(x)=1,\ 0<x<1;\qquad f_2(x)=e^{-x},\ 0<x<\infty;\qquad f_3(x)=\frac{1}{\pi(1+x^{2})},\ -\infty<x<\infty;
$$
$$
   f_4(x)=\frac{e^{-x}}{1-e^{-1}},\ 0<x<1;\qquad f_5(x)=\frac{4}{\pi(1+x^{2})},\ 0<x<1 .
$$
Determine the associated errors and analyse which ones reduce the variance of the integral estimate the most.


**Exercise 4**. Let $X\sim N(1,\sigma^{2})$. It is known that
   $$
   \left]\,\frac{(n-1)S_c^{2}}{\chi^{2}_{1-\alpha/2,\,n-1}}\ ,\ \frac{(n-1)S_c^{2}}{\chi^{2}_{\alpha/2,\,n-1}}\,\right[
   $$
is a $100(1-\alpha)\%$ confidence interval for $\sigma^{2}$. Using the Monte Carlo method, determine a confidence interval for $\sigma^{2}$.


**Exercise 5**. Consider a time series defined by $X_t=aX_{t-1}+Y_t$, where $Y\sim N(0,\sigma^{2})$. The least squares estimator of $a$ is given by
$$
   T=\frac{\sum_{t=2}^{n}X_tX_{t-1}}{\sum_{t=2}^{n}X_{t-1}^{2}} .
$$
Assuming the model with parameters $a=0.3$ and $\sigma^{2}=1$, a sample of 100 observations, and using the replication method (use 1000 replications):
**(a)** obtain an estimate of the parameter $a$;
**(b)** compute the standard deviation, mean squared error and bias associated with the estimate obtained; draw the boxplot of the sample of biases;
**(c)** determine a confidence interval for $a$.


**Exercise 6**. 
**(a)** Test $H_0:\sigma^{2}=4$ vs $H_1:\sigma^{2}>4$, at significance level $\alpha=0.05$. Using 100000 replications, obtain estimates of the significance level of the test, considering samples of size 100 from normal populations with unit mean, taking $\sigma^{2}=4$, $\sigma^{2}=10$ and $\sigma^{2}=1$. Comment on the results.
**(b)** Determine a confidence interval for $\sigma^{2}$, using the Monte Carlo method and data drawn from $N(1,4)$.

