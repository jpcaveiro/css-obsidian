# inverse transform method for uniform univariate continuous variables

Keywords: 
* [[univariate continuous variables]]
* [[uniform distribution (continuous)]]

To generate for any uniform distribution:


![[Pasted image 20260622162140.png]]

Exercises (a review of the previous slide):
1. [[explain]] the above development.
2. [[write pseudo code]] to get random values for distribution $U(a; b)$

> [!example]- solution
> Part 1: use $U=F_X(X)$.
> Part 2: [[algorithm]]
> - Get random values $u_i$ from $U(0;1)$.
> - Calculate $x_i = a+(b-a)u_i$.
> - return $x_i$ values that are random values from $U(a;b)$.

