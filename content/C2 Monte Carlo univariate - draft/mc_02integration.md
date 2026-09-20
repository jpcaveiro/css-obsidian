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


[[Memory is Something We Do]]:
* [[Ex 2-01]]
* [[Ex 2-02]] - A generalization of previous exercise.




