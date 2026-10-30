# Quality of MC simulations

This is a summary of indicators of the quality of simulations using Monte Carlo. 

Some of the below formulas make sense when exact $\theta$ is available, for example to inform the analytical development. In another set of formulas, the exact value $\theta$ can be replaced by its sample estimation $\hat \theta$.
## Integration goal with no replicas

A single sample, of size $n$, is generated to solve the problem of integration:

![[Pasted image 20261027144737.png]]

Simulation produces a sample $(g(x_1),g(x_2), \ldots, g(x_n))$ with $x_i$ sampled from $f(x)$ probability density function.

**Monte Carlo estimation** is 
$$\hat \theta = \frac{1}{n} \sum_{i=1}^n g(X_i)$$
with $X_i$ **sampled from** $f(x)$ probability density function as stated in $\theta$ integral.

The **absolute Monte Carlo error**, that needs exact value $\theta=E[g(X)]$, is
$$
\left|\frac{1}{n}\sum_{i=1}^{n}g(X_i)-E[g(X)]\right|
$$
(and, not so much used, but check the corresponding relative version: [[relative Monte Carlo error]]).

In what follows, consider a concrete sample $(x_1, \ldots, x_n)$ obtained from density $f(x)$.

**Sample variance** of the **simulated values** is
$$s^2_{g(X)} = \frac{1}{n} \sum_{i=1}^n (g(x_i)-\hat \theta)^2$$
or **sample standard error** of the **simulated values** is
$$s_{g(X)} = \sqrt{\frac{1}{n} \sum_{i=1}^n (g(x_i)-\hat \theta)^2}$$
The **Monte Carlo error**, (a short name for **Monte Carlo standard error**), is given by
$$\frac{s_{g(X)}}{\sqrt{n}}$$
and is an estimation of the analytical variance of the estimator $\hat \theta$
$$\sqrt{\text{Var}(\hat \theta)} = \sqrt{\text{Var}\left( \frac{1}{n} \sum_{i=1}^n g(X_i) \right)} = \sqrt{\frac{\text{Var}(g(X))}{n}} \text{ estimated by } \frac{s_{g(X)}}{\sqrt{n}}$$

(it is expected that $s_{g(X)}$ converges to a non null constant.)
## Using replicas in integration

In what comes, MC will generate $N$ sets of samples of size $n$:

* $X_1^{(1)}, X_2^{(2)}, \ldots,X_n^{(1)}$ (first sample of size $n$) will lead to **MC estimate** $\hat \theta^{(1)}$
* ... and so on ...
* $X_1^{(N)}, X_2^{(N)}, \ldots,X_n^{(N)}$ (last sample of size $n$)  will lead to **MC estimate** $\hat \theta^{(N)}$.

resulting in a, usual large, sample of estimations of $\theta$: $(\hat \theta^{(1)}, \hat \theta^{(2)}, \ldots, \hat \theta^{(N)})$.

Recall $\theta = E[g(X)]$. Now, its estimation is the mean over $N$ estimations:
$$\hat \Theta = \frac{1}{N} \sum_{i=1}^N \hat \theta^{(i)}$$based on the sample of estimations $(\hat \theta^{(1)}, \hat \theta^{(2)}, \ldots, \hat \theta^{(N)})$. 

In what follows consider using $\theta$ or $\hat \Theta$ according to the problem at hands: verifying analytical results and using exact $\theta$ or getting insights from a simulation when $\theta$ is not known:

Estimator $\hat \Theta$ is also unbiased so the quantity of interest is

$$\text{Var}(\hat \Theta) = \text{Var}\left(\frac{1}{N} \sum_{i=1}^N \hat \theta^{(i)}\right)=\frac{\text{Var}(\hat \theta^{(\cdot)})}{N}$$
that is **Monte Carlo standard error**
$$\sqrt{\text{Var}(\hat \Theta)} = \sqrt{\frac{\text{Var}(\hat \theta^{(\cdot)})}{N}} \text{ is estimated by } \frac{\text{sd}{(\hat \theta^{(1)}, \hat \theta^{(2)}, \ldots, \hat \theta^{(N)})}}{\sqrt{N}}$$
(it is expected that $\text{sd}(\hat \theta^{(1)}, \hat \theta^{(2)}, \ldots, \hat \theta^{(N)})$ converges to a non null constant.)


One can also choose **an appropriate plot** to see relation of the, usual large, sample of estimations of $\theta$: $(\hat \theta^{(1)}, \hat \theta^{(2)}, \ldots, \hat \theta^{(N)})$.

The replicating method is used in [[mc_statinference0_overview|inference]] (pointwise estimation, confidence interval and statistical hypothesis tests).

## Exercises

[[Memory is Something We Do]]

Exercise 1. [[Check]] that $\hat \theta$ is unbiased. (See definition above).

> [!example]- solution
> 
> One wants to check $E[\hat \theta] = \theta$. Notice that by definition $E[g(X)]=\theta$. So
> $$E[\hat \theta] = E\left[\frac{1}{n} \sum_{i=1}^n g(X_i)\right]=\frac{1}{n}(n \cdot E[g(X)]) = \theta$$


Exercise 2. [[Check]] that $\hat \Theta$ is unbiased. (See definition above).

> [!example]- solution
> Now we have several samples and its mean is $$\hat \Theta = \frac{1}{N} \sum_{i=1}^N \hat \theta^{(i)}$$
> So $$E[\hat \Theta] = E\left[\frac{1}{N} \sum_{i=1}^N \hat \theta^{(i)}\right]=\frac{1}{N}(N\cdot E[\hat \theta])=\frac{1}{N}(N\cdot \theta)=\theta$$


Exercise 3. [[Deduce]] that **Monte Carlo error** (a short name for **Monte Carlo standard error**), is $$\frac{s_{g(X)}}{\sqrt{n}}$$
> [!example]- solution
> $$\sqrt{\text{Var}(\hat \theta)} = \sqrt{\text{Var}\left( \frac{1}{n} \sum_{i=1}^n g(X_i) \right)} = \sqrt{\frac{\text{Var}(g(X))}{n}} \text{ estimated by } \frac{s_{g(X)}}{\sqrt{n}}$$

Exercise 4. [[Name]] these two quantities and [[explain]] why they are equal:
$$E\left[ (\hat\theta^{(i)}-E[\hat \Theta])^2 \right] \quad \quad \text{and} \quad \quad \frac{1}{N} \sum_{i=1}^N (\hat\theta^{(i)} - \hat\Theta)^2$$
> [!example]- solution
> The first follows definition of [[mean square error]] of $\hat \Theta$ estimator.
> The second is the sample variance of $\hat \theta$ estimator.
> This quantities are close because $E[\hat \Theta]=\theta$ ($\hat \Theta$ is unbiased).




