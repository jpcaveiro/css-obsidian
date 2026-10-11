# rejection method

Key concepts:
* [[univariate continuous variables]]

## Motivation for another method

Previous [[itm index|inverse transform method]] depends on the precise inverse CDF $F^{-1}(p)$. However, there are examples where the inverse CDF is impractical. These include the **normal distribution**, because its CDF has no simple closed-form inverse, and many **truncated or custom distributions**, where the CDF inverse must be computed numerically and can be slow or inaccurate.

The rejection method does not depend on inverse CDF. It uses an **existing** generation method for a distribution $g$, and then use it to generate random numbers for a distribution $f$ that is close to $g$, the one used by the existing method.

Rejection method is an efficient method if the functions f and g are similar (same means and similar domains) and is based on:

![[Pasted image 20260623145618.png]]

Note:
* The  $k g(x)$ is called "envelop" because it is above $f(x)$, the target distribution.
* Or, the graph of $kg(x)$ lies above the graph of $f(x)$ (pointwise).
![[Pasted image 20260926062215.png]]

[[Memory is Something We Do]]. Find a value for $k$ such that $g$ is the distribution $U(0;1)$ and $f(x) = 6x(1-x), \quad 0 \le x \le 1$.
> [!example]- a solution
> We need a constant such that:
> $$f(x) \le M g(x)$$
> for all values of x.
> Since:
> $$f(x) = 6x(1-x)$$ 
> has its maximum at $x = 0.5$ we get:
> $$f(0.5) = 6(0.5)(0.5) = 1.5$$
> So we can use: $M = 1.5$. The envelope is therefore:
> $$Mg(x) = 1.5$$
> This horizontal line sits above the target density everywhere on the interval from 0 to 1.



An [[algorithm]] could be:
![[Pasted image 20260623145929.png]]

[[Memory is Something We Do]]. Notice that $U$ is not from $U(0;1)$ but from $U(0; kg(x))$. Change the algorithm (a new [[write pseudo code|pseudo code]]) to use $U(0;1)$.
> [!example]- a solution
> ![[Pasted image 20260903084335.png]]


![[Pasted image 20260903084356.png]]

The **next chapter** will explore notion below related to the "acceptance probability" being $1/k$ in rejection method: 
* when generating a number $u$ from $U(0; kg(x))$, and accepting the outcome if $u\le f(x)$, then the proportion of acceptance is $\frac{f(x)}{kg(x)}$. The expectation of this proportion, when sampling from $g$, is
  $$\int_a^b \frac{f(x)}{kg(x)} g(x) dx=\frac{1}{k}$$
[[Memory is Something We Do]].
Exercise 1. Check 16/9 is a possible value for $k$ , using rejection method, to generate random values from [[beta distribution|beta(2,3)]], i.e., $f(x)=12x(1-x)^2$ for $0 \le x \le 1$, 
Exercise 2. [[write R code and run it]] to generate images like
![[Pasted image 20260903091955.png]] and ![[Pasted image 20260903092006.png]]

> [!example]- a solution
> [[C1 rejection method R code 01]]
>

Exercise 3. Generate PRN's from the [[Epanechnikov kernel density]] given by
$$f(x) = \frac{3}{4}(1 - x^2), \quad |x| \leq 1$$
Consider an auxiliary model for $g$ given by $U(-1, 1)$ distribution and show $k = 3/2$ is enough. Create similar graphics.


# Rejection method for truncated distribution

![[Pasted image 20260903095822.png]]

![[Pasted image 20260903095842.png]]

# Final comments

[[to do]] write about benefits and pitfalls of this method in the context of random number generation.

