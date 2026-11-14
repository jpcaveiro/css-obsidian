# MCMC Methods

* This file contains the original exercises, from Ex. 1 to Ex. 8, all about Markov Chain Monte Carlo methods and is based on "worksheet 3" from academic year 2025/26 .

---

**Exercise 1**. Consider the [[Rayleigh distribution]] with probability density function
   $$
   f(x)=\frac{x}{\sigma^{2}}e^{-x^{2}/(2\sigma^{2})},\qquad x\ge 0,\ \sigma>0 .
   $$
Use the Metropolis-Hastings algorithm to generate values from this distribution, taking as proposal function $q(y\mid x_t)$ the chi-square distribution with $x_t$ degrees of freedom. With $\sigma=4$ and 20000 replications, check whether the chain is efficient.


**Exercise 2**. The aim is to generate values from a target Student's $t$ distribution with $n$ degrees of freedom, using the random-walk Metropolis-Hastings algorithm with the normal distribution $N(0,\sigma^{2})$ for the random error (independent proposal function).
**(a)** Implement the Metropolis algorithm described, considering a chain of length $m=10000$, $\sigma=0.05$ and 4 degrees of freedom for the Student's $t$. Analyse its efficiency.
**(b)** Compare the results produced by the algorithm in terms of the number of rejections while varying $\sigma^{2}$, taking $\sigma^{2}=0.05;\,0.5;\,2;\,16$.
**(c)** Compare the quantiles of the theoretical (target) distribution --- Student's $t$ with 4 d.f. --- with the quantiles of the distribution of the generated values, for each of the values of $\sigma^{2}$ in the previous item and using a burn-in period of 1000. Draw conclusions.


**Exercise 3**. Consider a random sample $(Z_1,\dots,Z_n)$ from the following mixture of Normals:
   $$
   p\,N(\mu_1,\sigma_1^{2})+(1-p)\,N(\mu_2,\sigma_2^{2}) .
   $$
Assuming there is no information about $p$, the goal is to estimate the value of $p$ using $\operatorname{Beta}(1,1)$ distribution as the proposal function $g$, and assuming that the point $y$ generated in the Metropolis-Hastings algorithm is accepted with probability
   $$
   \alpha=\min\!\left(1,\frac{f(Y)g(X_t)}{f(X_t)g(Y)}\right)
   $$
--- this corresponds to the independence sampler.

Obtain an estimate of $p$ assuming that the generated values come from the mixture $0.2\,N(0,1)+0.8\,N(5,1)$.


**Exercise 4**. According to a genetic model, animals of a given species are distributed over 4 categories with probabilities
   $$
   p_1=\frac{2+\theta}{4},\quad p_2=\frac{1-\theta}{4},\quad p_3=\frac{1-\theta}{4},\quad p_4=\frac{\theta}{4},
   $$
where $0\le\theta\le 1$ is an unknown parameter about which inference is to be made. Assume that
- a [[beta distribution|beta]] prior distribution with parameters $(a,b)$ is adopted for $\theta$;
- for a sample of size $N$, $y_i$ animals were observed in the $i$-th category ($i=1,\dots,4$, $\sum y_i=N$).

The aim is to simulate from this distribution using the Metropolis-Hastings algorithm. If we use, for example, $q(\theta_i,\theta_j)=1$, this means that we simulate from uniforms and accept the simulated value with probability
   $$
   \alpha(\theta_i,\theta_j)=\min\!\left\{1,\frac{\pi(\theta_j\mid y)}{\pi(\theta_i\mid y)}\right\}.
   $$
Apply this algorithm to simulate from the distribution
   $$
   \pi(\theta\mid y)\propto(2+\theta)^{y_1}(1-\theta)^{y_2-y_3+b-1}\theta^{y_4+a-1},\qquad 0\le\theta\le 1,
   $$
taking $a=b=1$.


**Exercise 5**. In a bivariate normal model with mean vector $(\mu_1,\mu_2)$, variances $(\sigma_1^{2},\sigma_2^{2})$ and correlation $\rho$, consider the full conditional distributions
   $$
   X_1\mid X_2\sim N\!\left(\mu_1+\frac{\rho\sigma_1}{\sigma_2}(x_2-\mu_2),\,(1-\rho^{2})\sigma_1^{2}\right),
   $$
   $$
   X_2\mid X_1\sim N\!\left(\mu_2+\frac{\rho\sigma_2}{\sigma_1}(x_1-\mu_1),\,(1-\rho^{2})\sigma_2^{2}\right).
   $$
Use the Gibbs sampler to generate values from this bivariate normal, taking the parameter values $(\mu_1=0,\mu_2=2)$, $(\sigma_1^{2}=1,\sigma_2^{2}=0.25)$ and $\rho=-0.75$, and estimate the parameters through the corresponding sample characteristics.


**Exercise 6**. Suppose that $X=(X_1,\dots,X_n)$ is a sequence of random variables of the form $X_i=R_iY_i$, where the $Y_i$ are i.i.d. $\operatorname{Poisson}(\lambda)$ (see [[Poisson distribution]]), the $R_i$ are i.i.d. $\operatorname{Bernoulli}(p)$ (see [[bernoulli distribution]]), and $Y_i$ and $R_i$ are independent.

Given an observed sample $x=(x_1,\dots,x_n)$ of $X$, the goal is to estimate the parameters $(\lambda,p)$. From the Bayesian point of view, the following hierarchical model is considered:
- $p\sim U(0,1)$;
- $\lambda\mid p\sim Ga(a,b)$;
- $(r_i\mid p,\lambda)\sim Ber(p)$, independent;
- $(x_i\mid r,p,\lambda)\sim Poi(\lambda r_i)$, independent,
with $r=(r_1,\dots,r_n)$ and $a,b$ known constants. It follows that the joint distribution of $(x,r,\lambda,p)$ is
   $$
   f(x,r,\lambda,p)=\frac{b^{a}\lambda^{a-1}\exp(-b\lambda)}{\Gamma(a)}
   \prod_{i=1}^{n}\frac{\exp(-\lambda r_i)(\lambda r_i)^{x_i}}{x_i!}\,p^{r_i}(1-p)^{1-r_i}.
   $$
Simulations on $p$ and $\lambda$ can be carried out by simulating from the posterior distribution --- the distribution of $(r,\lambda,p)$ conditional on the observed data $x$ --- given by
   $$
   f(r,\lambda,p\mid x)=\frac{f(x,r,\lambda,p)}{\int f(x,r,\lambda,p)\,d(r,\lambda,p)} ,
   $$
using, for example, the Gibbs algorithm.
**(a)** The full conditionals have the form
   $$
   (\lambda\mid p,r,x)\sim Ga\!\left(a+\sum_i x_i,\ b+\sum_i r_i\right),
   $$
   $$
   (p\mid\lambda,r,x)\sim Be\!\left(1+\sum_i r_i,\ n+1-\sum_i r_i\right),
   $$
   $$
   (r_i\mid\lambda,p,x)\sim Ber\!\left(\frac{p\,e^{-\lambda}}{p\,e^{-\lambda}+(1-p)\mathbb{I}_{\{x_i=0\}}}\right).
   $$
   Prove the first two expressions.
**(b)** Generate a sample of size $n=100$ from the ZIP model using the parameters $p=0.3$ and $\lambda=2$.
**(c)** Implement the Gibbs algorithm to simulate from $f(r,\lambda,p\mid x)$ for the data of the previous item, obtain estimates of the parameters $p=0.3$ and $\lambda=2$, and characterise the distributions of $p\mid x$ and $\lambda\mid x$.


**Exercise 7**. McCormick and Mathew (1983) examined estimation questions related to the model
   $$
   X_t=\gamma+\rho X_{t-1}+Y_t,\qquad t\ge 1,
   $$
where $\gamma\ge 0$, $0\le\rho<1$ are unknown parameters and the $Y_t$ are i.i.d. random variables. The Bayesian analysis of this model when the $Y_t$ are exponential with mean $\alpha^{-1}$ was considered by Pereira and Amaral Turkman (1983). For a non-informative prior distribution, the posterior distribution based on a sample of size $n$ is
   $$
   h(\theta\mid x)\propto\alpha^{n-1}e^{-\alpha[S_0-\rho S_1-(n-1)\gamma]}\,\mathbb{I}_{\Theta_n}(\theta)
   $$
where $\theta=(\alpha,\gamma,\rho)$, $\Theta_n=\{\theta:\alpha\ge 0,\ 0\le\rho<1,\ \gamma\ge 0,\ x_t-\rho x_{t-1}-\gamma\ge 0,\ \forall t=1,\dots,n\}$, $S_0=\sum_{t=2}^{n}x_t$ and $S_1=\sum_{t=2}^{n}x_{t-1}$. Show that:

**(a)** The full conditional distributions are given by
   - $h(\alpha\mid x,\gamma,\rho)\sim Ga(n,\,S_0-\rho S_1-(n-1)\gamma)$;
   - $h(\gamma\mid x,\alpha,\rho)\sim Exp_{left}\!\left((n-1)\alpha,\gamma^{*}\right)$, where $\gamma^{*}=\min(x_t-\rho x_{t-1})$;
   - $h(\rho\mid x,\alpha,\gamma)\sim Exp_{left}\!\left(\alpha S_1,\rho^{*}\right)$, where $\rho^{*}=\min\!\left(1,\frac{x_t-\gamma}{x_{t-1}}\right)$.

   **Note:** $f(x)\sim Exp_{left}(\beta,\delta)$ means $f(x)=\dfrac{\beta e^{-\beta(\delta-x)}}{1-e^{-\beta\delta}}$, for $0<x<\delta$ (left-truncated exponential).
**(b)** The following data are dissolved-oxygen measurements taken at the Angeja bridge from June to November 1991:

| | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 4.0 | 4.1 | 3.9 | 4.4 | 3.2 | 4.0 | 3.7 | 4.2 | 4.5 | 4.3 | 3.6 | 1.9 |
| 3.3 | 1.9 | 2.9 | 2.7 | 2.4 | 2.9 | 3.8 | 3.5 | 2.7 | 3.9 | 2.8 | 3.3 |
| 2.9 | 3.8 | 4.4 | 5.1 | 5.2 | 7.2 | 6.2 | 4.8 | 4.0 | 2.7 | 4.4 | 3.4 |
| 4.2 | 4.8 | 5.3 | 4.5 | 4.1 | 4.0 | 2.9 | 0.8 | 5.2 | 7.3 | 5.1 | 5.3 |
| 7.1 | 8.1 | 7.8 | 6.9 | 7.5 | 6.0 | 5.0 | 5.3 | 4.8 | 4.3 | 5.8 | 4.6 |
| 4.5 | 4.1 | 4.6 | 6.4 | 6.3 | 6.2 | 6.2 | 6.8 | 7.5 | 7.4 | 7.0 | 6.7 |
| 7.5 | 6.1 | 5.7 | 5.4 | 5.3 | 4.0 | 3.7 | 2.5 | 0.8 | 1.3 | 3.3 | 4.1 |
| 5.7 | 4.3 | 3.5 | 3.8 | 2.0 | 3.8 | 4.1 | 1.8 | 3.0 | 4.7 | 6.2 | 6.0 |
| 5.3 | 4.4 | 3.4 | 4.7 | 4.5 | 3.7 | 4.3 | 1.6 | 2.9 | 3.6 | 3.7 | 3.9 |
| 4.6 | 5.0 | 5.3 | 4.7 | 6.5 | 5.7 | 5.8 | 8.0 | 7.4 | 6.1 | 7.6 | |

Using this sample, implement the Gibbs algorithm, using the `CODA` package to assess convergence, in order to estimate the parameters and approximately characterise the distributions of $\alpha\mid x$, $\gamma\mid x$ and $\rho\mid x$.


**Exercise 8**. Consider the following regression model (one-way random effects model with $k$ factors)
   $$
   Y_{i,j}=\mu+\alpha_i+\epsilon_{i,j},\qquad \alpha_i\sim N(0,\sigma_\alpha^{2}),\quad \epsilon_{i,j}\sim N(0,\sigma^{2}),
   $$
$j=1,\dots,n_i$; $i=1,\dots,k$. The model can also be written in hierarchical form, i.e.,
   $$
   Y_{i,j}\mid\alpha_i\sim N(\mu+\alpha_i,\sigma^{2})\quad\text{with}\quad \alpha_i\sim N(0,\sigma_\alpha^{2}) .
   $$
The joint density of $y\mid\mu,\alpha_1,\dots,\alpha_k,\sigma_\alpha^{2},\sigma^{2}$, with $y=(y_1,\dots,y_n)$, is given by
   $$
   \left(\frac{1}{\sigma_\alpha^{2}}\right)^{k/2}\exp\!\left[\frac{1}{2\sigma_\alpha^{2}}\sum_{i=1}^{k}\alpha_i^{2}\right]
   \left(\frac{1}{\sigma^{2}}\right)^{N_k/2}\exp\!\left[\frac{1}{2\sigma^{2}}\sum_{i=1}^{k}\sum_{j=1}^{n_i}(y_{ij}-\mu-\alpha_i)^{2}\right],
   \quad\text{with } N=\sum_{i=1}^{k}n_i ,
   $$
and the full conditional distributions are
   $$
   \alpha_i\mid y,\mu,\sigma_\alpha^{2},\sigma^{2}\sim
   N\!\left(\frac{n_i\sigma_\alpha^{2}}{n_i\sigma_\alpha^{2}+\sigma^{2}}(\bar{y}_i-\mu),\ \frac{\sigma_\alpha^{2}\sigma^{2}}{n_i\sigma_\alpha^{2}+\sigma^{2}}\right),\qquad i=1,\dots,k,
   $$
   $$
   \mu\mid y,\alpha_1,\dots,\alpha_k,\sigma_\alpha^{2},\sigma^{2}\sim N\!\left(\bar{y}-\bar{\alpha},\ \frac{\sigma^{2}}{N_k}\right),
   $$
   $$
   \sigma_\alpha^{2}\mid y,\alpha_1,\dots,\alpha_k,\mu,\sigma^{2}\sim
   IG\!\left(\frac{k}{2}-1,\ \frac{1}{2}\sum_{i=1}^{k}\alpha_i^{2}\right),
   $$
   $$
   \sigma^{2}\mid y,\alpha_1,\dots,\alpha_k,\mu,\sigma_\alpha^{2}\sim
   IG\!\left(\frac{N_k}{2}-1,\ \frac{1}{2}\sum_{i,j}(y_{ij}-\mu-\alpha_i)^{2}\right),
   $$
where $IG$ denotes the inverse gamma distribution.

Consider the following data, used to assess the precision of the estimated chemical composition of turnip leaves, where the leaves represent a random effect:

| factors | | | | |
|:---:|:---:|:---:|:---:|:---:|
| 1 | 3.28 | 3.09 | 3.03 | 3.03 |
| 2 | 3.52 | 3.48 | 3.38 | 3.38 |
| 3 | 2.88 | 2.80 | 2.81 | 2.76 |
| 4 | 3.34 | 3.38 | 3.24 | 3.26 |

Implement the Gibbs algorithm to obtain estimates of the parameters $\alpha_i$, $i=1,\dots,4$, $\mu$, $\sigma_\alpha^{2}$ and $\sigma^{2}$ (after assessing convergence) and some of their characteristics, and plot the corresponding full conditional distributions.
