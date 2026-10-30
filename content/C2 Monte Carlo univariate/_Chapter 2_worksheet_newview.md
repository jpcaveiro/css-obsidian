
# Worksheet 2: Monte Carlo Methods

* Transformed exercises that separate **concepts** and **implementation**.
* This file contains the original exercises but **only** from Ex. 1 to Ex. 7, all about Monte Carlo simulation and inference and are based on "worksheet 2" from academic year 2025/26 .

---

**Exercise 1**. Consider the goal of [[obtaining estimates (by simulation)]] of $p=P(X>2)$, with $X\sim Cauchy(0;1)$, i.e.,
   $$
   f(x)=\frac{1}{\pi(1+x^{2})},\qquad -\infty<x<\infty ,
   $$
Answer the following items.
**(a)** [[Define]] rare event. Is $X>2$ a rare event? (Use software.)
**(b)** [[Write an estimator]] using the standard [[Cauchy distribution]] as the random generator.
**(c)** [[Write an estimator]] using the [[Uniform distribution]] $(0; 2)$ as the random generator. Suggestion: what is the value $P(X > 0)$.
**(d)** [[Implement]] both estimators considering sample sizes of 100, 1000, 10000. Use seed=10.
**(e)** Explain, using [[mc_05howlarge|Chebyshev inequality]], why 100 iterations is probably not enough to achieve precision $\epsilon=0.001$ in both estimators.
**(e)** Fill the following table (it is known that $p\approx0.14758$) calculating "MC standard error" and "absolute MC error" (see definitions in [[mc_quality#Quality of MC simulations]]).

|               | MC standard error | absolute MC error |
| ------------- | ----------------- | ----------------- |
| estimator (b) |                   |                   |
| estimator (c) |                   |                   |



**Exercise 2**. The aim is to compute the value of the integral
   $$
   I=\int_{0}^{\infty}\log(x)\,x^{5}e^{-3x}\,dx .
   $$
Using the Monte Carlo integration method:
**(a)** [[Write an estimator]] using the distribution $X\sim Exp(3)$.
**(b)** [[Write an estimator]] using the distribution $X\sim Ga(6,3)$.
**(c)** How to use the replication method to estimate $I$ with $X\sim Ga(6,3)$? 
**(d)** [[Implement]] both estimators considering sample sizes, $n$, of 100, 1000, 10000, and for (c) also use $N=1000$. Use seed=10. 
**(e)** It is known that $I=0.1000009$. Determine the MC standard error and the absolute MC error for each $N$ with methods (a), (b) and (c).


**Exercise 3**. The aim is to [[Obtain estimates (by simulation)|estimate the integral]]
$$
I = \int_{0}^{1}\frac{e^{-x}}{1+x^{2}}\,dx
$$
using the importance sampling technique. 
**(a)** [[Show how]] importance sampling technique can be used to reduce estimator variance (see [[LLM C2 importance sampling]]).
**(b)** Consider the following candidate importance functions:
$$
   f_1(x)=1,\ 0<x<1;\qquad f_2(x)=e^{-x},\ 0<x<\infty;\qquad f_3(x)=\frac{1}{\pi(1+x^{2})},\ -\infty<x<\infty;
$$
$$
   f_4(x)=\frac{e^{-x}}{1-e^{-1}},\ 0<x<1;\qquad f_5(x)=\frac{4}{\pi(1+x^{2})},\ 0<x<1 .
$$
[[Write an estimator]] for $I$ considering each proposal density function $f_i$.
**(c)** [[Implement]] each estimator and determine the MC standard error and the absolute MC error and analyze which ones reduce the variance of the integral estimate the most.


**Exercise 4**. Let $X\sim N(1,\sigma^{2})$. It is known that
   $$
   \left]\,\frac{(n-1)S_c^{2}}{\chi^{2}_{1-\alpha/2,\,n-1}}\ ,\ \frac{(n-1)S_c^{2}}{\chi^{2}_{\alpha/2,\,n-1}}\,\right[
   $$
is a $100(1-\alpha)\%$ confidence interval for $\sigma^{2}$. 
**(a)** [[Explain]] how to use Monte Carlo method with replicas to determine a confidence interval for $\sigma^{2}$.
**(b)** [[Implement]] it using several values for $N$ (100, 1000, 10000).


**Exercise 5**. Consider a time series defined by $X_t=aX_{t-1}+Y_t$, where $Y\sim N(0,\sigma^{2})$. The least squares estimator of $a$ is given by
$$
   T=\frac{\sum_{t=2}^{n}X_tX_{t-1}}{\sum_{t=2}^{n}X_{t-1}^{2}} .
$$
Assuming the model with parameters $a=0.3$ and $\sigma^{2}=1$, a sample of $n=100$ observations, and using the **replication** method (use $N=1000$ replications).
**(a)** [[Explain]] all steps of how to get an estimator for $a$ using **replication** method.
**(b)** [[Implement]] the procedure and obtain an estimate of the parameter $a$;
**(c)** [[Write an expression]] for the Monte Carlo error (see [[mc_quality]]) and [[Implement]] it.
**(d)** [[How to]] determine a confidence interval for $a$ at 95%? 
**(e)** [[Implement]] previous answer and calculate the confidence interval.
**(f)** Considering the Monte Carlo replication estimator, [[Write an expression]] for: [[mean square error]], standard deviation and bias, associated with the replication estimator. Use the exact value of the parameter $a$, **or**, use estimation $E[T] \approx \bar T$ when appropriate because $T$ is not a centered estimator for small $n$. 
**(g)** [[Implement]] previous quantities and draw the boxplot of the sample of biases;


**Exercise 6**. 
**(a)** Test $H_0:\sigma^{2}=4$ vs $H_1:\sigma^{2}>4$, at significance level $\alpha=0.05$. Using 100 000 replications, obtain estimates of the significance level of the test, considering samples of size 100 from normal populations with unit mean, taking $\sigma^{2}=4$, $\sigma^{2}=10$ and $\sigma^{2}=1$. Comment on the results.
**(b)** Determine a confidence interval for $\sigma^{2}$, using the Monte Carlo method and data drawn from $N(1,4)$.

> [!sample]- a solution
> [[LLM C2 Worksheet 2 Exercise 6]]

