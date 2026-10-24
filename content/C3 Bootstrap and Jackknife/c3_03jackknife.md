# Jackknife technique

The jackknife method is primarily used to **reduce bias** in statistical estimates and to **estimate variance (standard error)** when standard theoretical formulas are unavailable or unreliable.

In what follows, jackknife samples $\hat \theta^{(j)}$ are not directly used to estimate $\theta$ but to estimate the bias of an estimation $\hat \theta$ when we have a sample but not have a closed expression for bias.

Generally, bias of an estimator $\hat \theta$ is defined by: $\text{bias}(\hat \theta) = E[\hat \theta] − \theta$ with $\theta$ the unknown parameter.

In jackknife setting, one has a method of estimation of bias, $\widehat{bias}(\hat \theta)$, and using $\hat \theta$ as an estimate for $E[\hat \theta]$.  From bias definition, the jackknife estimation is given by: 
$$\hat \theta_{jack} = \hat \theta - \widehat{bias}(\hat \theta)$$

![[Pasted image 20260720153319.png]]

Notation description:
* $X^{(j)}$ is original sample without element $X_j$.
* $\hat \theta_{n-1}$ is the estimate based on $n-1$ elements from $X^{(j)}$
* $\hat \theta^{(j)}$ is another symbol for $\hat \theta_{n-1}(X^{(j)})$.
* $\hat \theta_n$ is the  estimate based on original sample.


![[Pasted image 20260720160859.png]]

Notation description:
* $\hat \theta^{(\cdot)}$ is a sample of jackknife estimations of size $n-1$
* $\overline{\hat \theta^{(\cdot)}}$ is the mean of the above estimations
* $\hat \theta_n$ is the  estimate based on original sample.

[[math result]]
![[Pasted image 20260721082533.png]]
Notation description:
* $\hat \theta^{(\cdot)}$ is a sequence of jackknife estimations
* $\overline{\hat \theta^{(\cdot)}}$ is the mean of the above estimations
* $\hat \theta_n$ is the  estimate based on original sample.

![[Pasted image 20260721082831.png]]


[[definition]] jackknife estimate for the standard deviation of $\hat \theta_n$:
![[Pasted image 20260721083008.png]]
Notation description:
* $\hat \theta^{(j)}$ is a the jackknife estimation taking element $j$ out
* $\hat \theta^{(\cdot)}$ is a sequence of jackknife estimations (all $j$)
* $\overline{\hat \theta^{(\cdot)}}$ is the mean of the above estimations
* $\hat \theta_n$ is the  estimate based on original sample.


[[Memory is Something We Do]]

Install [[bootstrap R package]] and load `patch` data frame using `data(patch)`.

Exercise 1. Solve the example 3.1:
![[Pasted image 20260721082917.png]]

Exercise 2. Solve the example 3.2:
![[Pasted image 20260721083700.png]]


> [!example]- solution to both exercises and conclusion
> ![[Pasted image 20260721082942.png]]
> 
> So, $|\hat \theta| \approx 0.0713061$  that is $\le 0.2$ suggesting bioequivalence. Bias estimate is 0.008. 
> 
> ![[Pasted image 20260721083733.png]]
> 
> Since bias and standard error, of the estimate $\hat \theta$, are both small then above conclusion follows.  The correction of $\hat \theta$ estimate is -0.0713061 - 0.008 = -0.0793061, so $|\hat \theta_{jack}| \le 0.2$.


[[Further reading]]:
* [[LLM C3 more on jackknife]]

