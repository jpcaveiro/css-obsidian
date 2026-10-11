# Inverse transform method for univariate discrete variables

Keywords: 
* [[univariate discrete variables]]


![[Pasted image 20260622170206.png]]


The [[algorithm]] to generate random variables is:
![[Pasted image 20260622170226.png]]

[[Memory is Something We Do]]

Exercise 1. [[what]] are the $x_i$ values from image distribution?

Exercise 2. [[give one reason]] of why $F_X(x_{i-1}) < u \le F_X(x_i)$ and not  $F_X(x_{i-1}) \le u < F_X(x_i)$.

Exercise 3. [[hand plot]] $x_i$ for $u \in [0,1]$ for the example.



[[definition]] Define the generalized inverse $F^{-1}(u)=\inf\{x: F(x)\ge u\}$ for a discrete random variable with support $\{x_1<x_2<\cdots\}$.

Some art:
![[Pasted image 20260930103326.png]]



To generate from [[univariate discrete variables]] consider:

![[Pasted image 20260622170652.png]]

[[Memory is Something We Do]].

Exercise 1. [[Show]] that $F^{-1}(U)\sim F$ .

Exercise 2. [[explain]] the following slide:

![[Pasted image 20260622172417.png]]


A generalization of the algorithm is:

![[Pasted image 20260622172547.png]]

[[Memory is Something We Do]].

Exercise 1. [[write R code and run it]] to implement the the generalized invers $F^{-1}(u)$ based on the above slide and for any discrete distribution function:
```r
generalized_inverse <- function(u, x_vector, p_vector) {

return x
}
```


[[Further reading]]: [[LLM C1 discrete inverse]]
