# inverse transform method for exponential variables

Keywords:
* [[univariate continuous variables]]

To generate for any exponential distribution:

![[Pasted image 20260622164358.png]]

[[Memory is Something We Do]].

Exercise 1. [[Show]] that $U \sim U(0;1)$ then $1-U \sim U(0;1)$ and [[explain]] why this may be useful.


Get random values for distribution $Exp(\lambda)$ with the following [[algorithm]]:

1. Get random values $u_i$ from $U(0;1)$.
2. Calculate $x_i = -\frac{1}{\lambda} \ln u_i$.
3. $x_i$ values are random values from $Exp(\lambda)$.

Consider the following code and output of [[R code]]:

![[Pasted image 20260622164750.png]]

 [[Memory is Something We Do]].

 Exercise 1. [[write R code and run it]] (previous code).
