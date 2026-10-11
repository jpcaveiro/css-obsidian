# MC application to Integration

Monte Carlo integration algorithm


![[Pasted image 20260716113230.png]]

![[Pasted image 20260716113243.png]]

Generally, to get a MC estimate of the integral
$$
I=\int_{\mathcal{X}} h(x)\,dx,
$$
one must express a $h$ in a different manner. A decomposition is needed:
$$
h(x)=g(x)f(x)
$$
with $f(x)$ being the *pdf* of a random variable with support $\mathcal{X}$. Then,
$$
I=\int_{\mathcal{X}}h(x)\,dx
=\int_{\mathcal{X}}g(x)f(x)\,dx
=\mathbb{E}[g(X)].
$$


[[Memory is Something We Do]].

Exercise 1. 
![[Pasted image 20260716113325.png]]
**(a)** Calculation of $\theta$ using MC needs that the integral be written with a density $f(x)$: 
$$\theta = \int_0^1 e^{-x}  f(x) dx$$
[[Write density]] $f(x)$ to be used in integral from which to generate $x_1, x_2, \ldots,x_n$ samples
**(b)** [[write R code and run it]] and compare with several $m$ values:

> [!example]- solution
> **(a)** [[to do]]
> **(b)** 
> ![[Pasted image 20260716162918.png]]
> [[to do]] an histogram


Exercise 2.
![[Pasted image 20260716163135.png]]

**(a)** [[rewrite]] integral to use MC sampling with the following density $f_U(x)$ :

![[Pasted image 20260716171739.png]]
> [!example]- a solution for item A
> 
>![[Pasted image 20260716173229.png]]

**(b)** [[apply]] item A to rewrite integral and to estimate $\theta$ for concrete case:
![[Pasted image 20260716174852.png]]

> [!example]- a solution for item B
> Use $f_U(x) = \frac{1}{b-a}$,  or $U \sim U(a=2; b=4)$, to get samples $u_1, \ldots, u_n$.
> $$\int_2^4 e^{-x} dx = (4-2) \int_2^4 e^{-x} f_U(x) dx$$
 
**(c)** Consider the general case $\int_a^b e^{-x} dx$. [[Estimate]] $\theta$ using Monte Carlo with only two "random" values $x_1=a$ and $x_2=b$ (make $n=2$).

> [!example]- a solution for item C
> $$\hat \theta = (b-a) \frac{1}{2}(e^{-a}+e^{-b})$$
 
**(d)** [[What]] is the estimator $\hat \theta$ in terms of [[numerical integration]]? Interpret both solutions.

> [!example]- a solution for item D
> Its the trapezoidal rule where:
> - (b-a) is the base of the trapezoid
> - $\frac{1}{2}(e^{-a}+e^{-b})$ is the mean height.
> 
> In terms of Monte Carlo method:
> - (b-a) is the base of the trapezoid
> - $n=2$ with $x_1$ and $x_2$ are random values
> - then $\frac{1}{2} \sum_{i=1}^{2} e^{x_i}$,  make a estimator of the mean of $e^{-x}$ in $[a;b]$ set.

**(e)** [[write R code and run it]] to implement the following integral

![[Pasted image 20260716172216.png]]

 > [!example]- a solution for item E
 > ![[Pasted image 20260716182112.png]]
 > [[to do]] histogram



[[Further reading]]: 
* Mean Value Theorem for Integrals and Monte Carlo - [[LLM C2 MVTI vs MC]]

 



