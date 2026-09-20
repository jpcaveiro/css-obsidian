# Inverse transform method for univariate discrete variables

Keywords: 
* [[univariate discrete variables]]

## Summary

![[Pasted image 20260622170206.png]]


The [[algorithm]] to generate random variables is:
![[Pasted image 20260622170226.png]]

Exercises:
1. [[what]] are the $x_i$ values from image distribution?
2. [[give one reason]] of why $F_X(x_{i-1}) < u \le F_X(x_i)$ and not  $F_X(x_{i-1}) \le u < F_X(x_i)$.
3. [[plot]] $x_i$ for $u \in [0,1]$ for the example.



## Concepts
![[Pasted image 20260622170652.png]]

* $u$ is generated from $U(0;1)$;
* recall that $u$ **can be seen as a probability** $p$.  When $U \sim Unif(0;1)$, $F_U(u)=u$ shows that $u$ is also a probability.


![[itm_udv_img1.pdf]]

Exercise:
1. [[explain]] the following slide

![[Pasted image 20260622172417.png]]
(slide paper nr 17)

## Generalization

![[Pasted image 20260622172547.png]]

Exercise:
1. [[write R code and run it]] to implement the above slide.

Continuation:
* [[itm udv binomial|special case: binomial]]
* [[itm udv poisson|special case: Poisson]]

