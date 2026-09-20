# inverse transform method for exponential variables

Concepts and Keywords:
* [[univariate continuous variables]]

## Summary

[[algorithm]] Get random values for distribution $Exp(\lambda)$:

2. Get random values $u_i$ from $U(0;1)$.
3. Calculate $x_i = -\frac{1}{\lambda} \ln u_i$.

* $x_i$ values are random values from $Exp(\lambda)$.
 
 Exercise: 
 1. [[write pseudo code]] again.
## Proof

![[Pasted image 20260622164358.png]]

Exercise:
1. [[explain]] deductions.

## Numerical example
[[R code]]
![[Pasted image 20260622164750.png]]

Exercises:
1. [[explain]] code in detail.
2. [[run R code]] like the example 
