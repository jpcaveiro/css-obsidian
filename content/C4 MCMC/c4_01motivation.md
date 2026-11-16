# Motivation

[[motivation]]
We still want to calculate 

$$
\frac{1}{n} \sum g(x_i) \mapsto_{n\to \infty} E[g(X)]
$$
with $x_i$ taken as random values from a target distribution $f$.

![[Pasted image 20260721102346.png]]

![[Pasted image 20260721102526.png]]

![[Pasted image 20260721102634.png]]

target function:
* $f(x)$ is a "target function" $f$ is the density from which we want to generate random samples.
* applies to the multidimensional case.

video examples :

* https://youtu.be/U561HGMWjcw?si=oxpFkYsZMEpOdlHm&t=295 (1D e 2D) - (after middle)
* https://youtu.be/3qodjHRUxAo?si=xJImrn_vA5p8JX9e (in this video the word "kernel" should be "proposal". See [[LLM C4 more on Markov kernel]].)

The above slide mentions "correlated variables". Read more important explanation in [[LLM C4 MCMC correlation vs independence]].

