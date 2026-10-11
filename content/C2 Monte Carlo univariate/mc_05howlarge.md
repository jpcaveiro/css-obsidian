
# MC Estimation Accuracy

![[Pasted image 20260717103641.png]]


![[Pasted image 20260717103806.png]]

Before the next slide, consider the following useful definitions:
![[absolute Monte Carlo error]]

## How to find $N$?

In what follow:

* $\epsilon$ is the **requested** limit of the [[absolute Monte Carlo error]] (a precision)

then

* $N$ is the **necessary number** of samples needed to a certain [[absolute Monte Carlo error]]

 If $N$ is enough then $\left|\frac{1}{N}\sum g(X_i) - E[G(X)]\right|\le \epsilon$. 
 
To find $N$ one uses the [[Chebyshev inequality]]:

![[Pasted image 20260919112321.png]]

Now we introduce constant $\alpha$. This constant is chosen by user  and is usually a small value. In statistics the expression $1 - \alpha$ is usually set to be 0.95 or 0.99.

By now, user sets $\epsilon$ (a small value) and $1-\alpha$. How to use $1 - \alpha$?

As in confidence intervals, set right hand side of the inequality, with a fixed known (or given) constant described by expression $1 - \alpha$  such that
$$
1 - \frac{Var(g(X))}{N \epsilon^2} \ge 1- \alpha
$$
and so $\alpha$ should be 
$$
\alpha \ge \frac{Var(g(X))}{N\epsilon^2}
$$
or, swapping $\alpha$ and $N$,
$$
N \ge \frac{Var(g(X))}{\alpha\epsilon^2}
$$
When simulating values of  $\epsilon$ and $\alpha$ are set according to needs and so one has a lower bound for $N$ if we know $V(g(X))$ as states above.

Summarizing, 

![[Pasted image 20260919014310.png]]

Now, consider the case where a maximum value of variance is known: that is $V(g(X))< V_{max}$. Then, if 
* $N \ge \frac{V_{max}}{\alpha \epsilon^2}$ 
then for actual $V$ the inequality is also valid
* $N \ge \frac{V}{\alpha \epsilon^2}$.



Example:
![[Pasted image 20260919013917.png]]


![[Pasted image 20260717104833.png]]

