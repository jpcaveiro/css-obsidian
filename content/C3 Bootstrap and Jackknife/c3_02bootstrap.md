# Bootstrap technique

The **bootstrap method** is a computer-intensive statistical technique that estimates the sampling distribution of a statistic $\hat \theta$ by repeatedly resampling **with replacement** from your observed data.

First, read the following summary of the method:
* [[LLM C3 bootstrap method]]

![[Pasted image 20260720104851.png]]



![[Pasted image 20260720105529.png]]

* Random variable $X$ follows $F$ distribution function and a sample of size $n$ produces empirical distribution designated by $F_n$
* Random variable $X\star$ follows $F_n$ distribution function and a sample of size $n$ produces empirical distribution designated by $F\star_n$

The image is showing the two main ways to think about the bootstrap in statistics. It contrasts the **true data-generating process** with the **empirical resampling process** used in practice. 

A simple way to read the picture is: 
* **real world** $\to$ observed sample $\to$ estimated distribution, then,
* **estimated distribution** $\to$ resampled data $\to$ bootstrap version of the distribution.

What the arrows mean:

- $F \to X \to F_n$: **this is the usual statistical story**.
- $F$ is the unknown true population distribution (in the bootstrap method).
- $X$ is the observed sample drawn from an unknown $F$.
- $F_n$ is the empirical distribution built from that sample. 

- $F_n \to X^* \to F_n^*$: **this is the bootstrap story**.
- Start from the empirical distribution $F_n$, not the unknown $F$.
- Draw a bootstrap sample $X^*$ from $F_n$, with replacement.
- Compute the bootstrap empirical distribution $F_n^*$ from that resample.

The ideia: the bootstrap replaces the unknown population distribution $F$ with the empirical distribution $F_n$ estimated from your data. Then it repeatedly resamples from $F_n$ to mimic what new samples from $F$ might look like. 

## Inference with bootstrap

Next slide is about an estimator $\hat \theta$ whose estimates are calculated for each bootstrap sample $\hat \theta (x^{\star (b)})$. From each bootstrap sample $x^{\star(b)}$, one gets an estimate $\hat\theta^{(b)}$, $b=1, \ldots,B$:

![[Pasted image 20260720110356.png]]

Notation description:
* $B$ - number of bootstrap samples
* $b$ is a number in 1, ..., B
* $x^{\star(b)}$ is the b<sup>th</sup> bootstrap sample (with replacement)
* $\hat \theta^{(b)}$ is the estimate of a parameter $\theta$ using $x^{\star(b)}$
* $F_{\hat \theta}$ empirical distribution of the estimations $\hat \theta^{(i)}$, $i=1,\ldots,B$

## Bias in bootstrap method

Recall [[bias]]:
$$\text{bias}(\hat \theta) = E[\hat \theta] − \theta$$

We need
* $\hat \theta = \hat \theta(x_1, \ldots,x_n)$ is the estimation of $\theta$ **based on original sample** (not on bootstrap sample).
* $\overline{\hat \theta^{\star}}$ is the average of the B estimations $\hat \theta^{(b)}$

The value of $\theta$ is not known in bootstrap setting so one replaces $\theta$ by $\hat \theta$  and $E[\hat \theta]$ by $\overline{\hat \theta^{(b)}}$: 

![[Pasted image 20260720150801.png]]


Using the same notation, the standard deviation of the estimation is calculated by:

![[Pasted image 20260720153113.png]]


[[Memory is Something We Do]]

In what follows, consider the [[Pearson correlation coefficient]] and its characteristics.
  
Exercise 1. Solve the following example.
![[Pasted image 20260720153016.png]]
Note: there are two databases: `law` (a sample) and `law82` (all population). Use the shortest one loading to memory `data(law)` and then using dataframe `law`.

> [!example]- solution
> ```r
> library(bootstrap)
> data(law)
> # Estimativa Bootstrap do viés do
> # coeficiente de correlação R
> 
> # estimativa para a amostra law de dimensão n=15
> theta.hat <- cor(law$LSAT, law$GPA)
> 
> # estimativa bootstrap do viés
> B <- 2000 # número de réplicas bootstrap
> n <- nrow(law)
> theta.b <- numeric(B)
> for (b in 1:B) {
>     i <- sample(1:n, size = n, replace = TRUE) # i é o vector dos índices
>     LSAT <- law$LSAT[i]
>     GPA <- law$GPA[i]
>     theta.b[b] <- cor(LSAT, GPA)
> }
> bias <- mean(theta.b) - theta.hat
> bias
> # output
> #> bias
> #[1] 0.007822616
> ```


Exercise 2. Solve the following example.
![[Pasted image 20260720153155.png]]

Note: for this, load data with `data(law82)` and test writing `law82` on R.

> [!example]- solution
> ![[Pasted image 20260720153227.png]]
> ![[Pasted image 20260720153245.png]]
> ![[Pasted image 20260720153257.png]]



[[Further reading]]:
* [[LLM C3 why bootstrap name]]
