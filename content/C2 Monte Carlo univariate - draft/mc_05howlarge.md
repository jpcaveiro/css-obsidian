
# MC Estimation Accuracy

![[Pasted image 20260717103641.png]]


![[Pasted image 20260717103806.png]]

Before the next slide, consider the following useful definitions:
![[absolute Monte Carlo error]]

## How to find $N$?

* $\epsilon$ is the limit of the [[absolute Monte Carlo error]] (a precision).
* $N$ is the necessary number of samples needed to a certain [[absolute Monte Carlo error]]:
	* if $N$ is enough then $\left|\frac{1}{N}\sum g(X_i) - E[G(X)]\right|\le \epsilon$.

![[Pasted image 20260919112321.png]]

In statistics the expression $1 - \alpha$ is usually set to be 0.95 or 0.99. Set the right part to be big and define $\alpha:=\alpha(N)$ such that
$$
1 - \frac{Var(g(X))}{N \epsilon^2} \ge 1- \alpha
$$
and then $\alpha$ should be 
$$
\alpha \ge \frac{Var(g(X))}{N\epsilon^2}
$$
so
$$
N \ge \frac{Var(g(X))}{\alpha\epsilon^2}
$$
so we get 

![[Pasted image 20260919014310.png]]

Now, consider that $V(g(X))< V_{max}$. Then, if $N \ge \frac{V_{max}}{\alpha \epsilon^2}$ one guarantees $N \ge \frac{V}{\alpha \epsilon^2}$:

![[Pasted image 20260919113921.png]]


![[Pasted image 20260919013917.png]]


![[Pasted image 20260717104833.png]]

