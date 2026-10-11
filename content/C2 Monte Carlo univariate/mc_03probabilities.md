# MC application to Probabilities

Using MC integration how can we approximate probabilities $P(X \in A)$?

An easy solution is:

![[Pasted image 20260717084543.png]]

For example, 

![[Pasted image 20260717084558.png]]


## Problem with rare events

Naturally, rare events are those with very small probabilities.

![[Pasted image 20260717084703.png]]


A solution to the problem is the [[mc_04importancesampling|importance sampling]] technique in the next section but first do the exercise.

[[Memory is Something We Do]].  Let $X \sim N(0; 1)$.
**(a)** Estimate $P(X \le 2)$ and $P(X \ge 2)$ and [[write R code and run it]] to illustrate the difference between the exact and estimated results.

> [!example]- a solution
> [[to do]] using LLM, for example, Write r script to generate 1000 random samples from N(0,1) and calculate probability of P(X >=4)


**(b)** Estimate $P(X \le 4.5)$ and $P(X \ge 4.5)$ and:
* [[write R code and run it]] to illustrate the difference between the exact and estimated results.
* [[What]] is the "danger" of the estimated results.
* [[Empirically find]] $n$ (number of samples) to avoid 0 and 1 estimated results.

> [!example]- solution with code
> ![[Pasted image 20260717094454.png]]
> ![[Pasted image 20260717095112.png]]
> ![[Pasted image 20260717101533.png]]
> 


[[Further reading]]: 
* [[LLM C2 difference between two probabilities]]

