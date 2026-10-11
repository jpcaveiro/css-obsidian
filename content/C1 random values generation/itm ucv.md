# inverse transform method for general univariate continuous variables

Revision and key concepts: 
* [[univariate continuous variables]]
* [[uniform distribution (continuous)]]
## Using an uniform distribution to get random values

[[Memory is Something We Do]]:

Exercise 1. Consider the image from wikipedia and [[explain]] dots in both Y and X axis considering that:
- in the image $F_X$ is an [[exponential distribution]] with mean $1/\lambda$;
- notice uniformly points in Y axis.
![a|500x400](https://upload.wikimedia.org/wikipedia/commons/5/5a/Inverse_transformation_method_for_exponential_distribution.jpg)

Exercise 2. [[Explain]] the [animation from wikipedia](https://en.wikipedia.org/wiki/File:Inverse_Transform_Sampling_Example.gif).

> [!example]- possible answer
> [[to do]]
## Propositions

Let $X$ be a continuous r.v. with distribution function $F_X$. 
Let $U$ be a continuous r.v. with distribution function $U(0;1)$. 

Consider now:
![[Pasted image 20260902095538.png]]

[[Memory is Something We Do]]:

Exercise 1. If $P(Y\le y)=y$ what is the [[name|known distribution]] of $Y$? (repeat!)

Exercise 2. [[Check]] that if $X \sim F_X$ then $F_X(X)\sim U(0;1)$, i.e., random variable $Y=F_X(X)$ has uniform distribution $U(0; 1)$.

Exercise 3. [[Check]] that if $U \sim U(0;1)$ then $F^{-1}(U) \sim F_X$, i.e, having random variables from U one can get random values from $F_X$.

> [!example]- solution
> Exercise 1
> $Y \sim U(0;1)$ because its the only solution.
> 
> Exercise 2
> Consider $y$ a real number. 
> Consider $Y=F_X(X)$.
> Then
> 
> $$P(Y\le y)=P(F_X(X)\le y) = P(X \le F^{-1}_X(u)) = F(F^{-1}_X(u))=y$$
> Since $P(Y \le y)=y$ then $Y \sim U(0;1)$, then $F_X(X)\sim U(0;1)$
> 
> Exercise 3
> $$P(F^{-1}_X(U) \le z) = P(U \le F_X(z)) = P(X \le z) = F_X(z)$$
> then $F^{-1}_X(U)$ has distribution $F_X$.
> See also
> ![[Pasted image 20260624155546.png]]
> 

## Algorithm to generate random numbers

To get random values for any continuous distribution $F_X$ one can implement the following [[algorithm]]:
```
Get random values $u_i$ from $U(0;1)$.
Calculate $x_i = F^{-1}_X(u_i)$.
Return $x_i$ values that constitute random values from $F_X$.
```

![[Pasted image 20260622162057.png]]

[[Memory is Something We Do]].

Exercise 1. [[write R code and run it]] to implement for some given continuous distribution function:
```r
  rand_gen = function(dist_fun, samplesize) {
  # dist_fun is a function distribution like `pnorm`, `pexp` (continuous):
  # Example: rand_gen(pnorm, 10) will generate 10 normal random numbers.
  
  # Algoithm:
  # generate from U(0;1)
  # make random values  
  
	  
	return rvals
  }
```
> [!example]- a solution 
> [[to do]]

