 [[to do]] Explain how to get real $\theta$ in expressions below?

# bias and mean square error

Recall, MC will generate $N$ sets of samples of size $n$:

* $X_1^{(1)}, X_2^{(2)}, \ldots,X_n^{(1)}$ (first sample of size $n$)
* ... and so on ...
* $X_1^{(N)}, X_2^{(N)}, \ldots,X_n^{(N)}$ (last sample of size $n$).

# parameters

Notice that in slide there is a **little redundancy** in notation between $T^{(i)}$ and $\hat \theta^{(i)}$:

![[Pasted image 20260717114025.png]]

Now, **suppose $\theta$ is known in next slides** and we want to estimate [[bias of a estimator|bias]] and [[mean square error]]:

![[Pasted image 20260717113829.png]]

# example

Suppose 
$$
X_1,\ldots,X_n\sim \operatorname{Uniform}(0,\theta),
$$
and we use
$$
\hat{\theta}=2\bar X
$$
to estimate $\theta$. This estimator is unbiased because
$$
E[\bar X]=\frac{\theta}{2}
$$
and therefore
$$
E[\hat{\theta}]
=
E[2\bar X]
=
2\frac{\theta}{2}
=
\theta.
$$
A Monte Carlo procedure would be:

1. Choose a value, say $\theta=10$.
2. Generate $N$ samples of size $n$ from $\operatorname{Uniform}(0,10)$.
3. For each sample, calculate $\hat{\theta}^{(i)}=2\bar X^{(i)}$.
4. Compute
$$
\widehat{\operatorname{Bias}}(\hat{\theta})
=
\frac{1}{N}\sum_{i=1}^N\hat{\theta}^{(i)}-10.
$$
For sufficiently large $N$, the result should be close to $0$.






