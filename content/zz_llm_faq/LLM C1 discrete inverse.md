The generalized inverse is
$$
F^{-}(u)=\min\{x : F(x)\ge u\},\qquad u\in(0,1),
$$
which is the same notation as your C1 notes. Please consider the notation:  $F^-$ and not $F^{-1}$.

The claim to prove is that $X=F^{-}(U)$ with $U\sim\text{Uniform}(0,1)$ satisfies $P(X\le x)=F(x)$.

## Setup

- Support: $x_1<x_2<x_3<\dots$, with $p_k=P(X=x_k)$.
- CDF at the support points: $F(x_k)=p_1+\dots+p_k$. Set $F(x_0)=0$.
- $F$ is a non-decreasing step function. It is constant on each interval $[x_k,x_{k+1})$, so the minimum over $\{x: F(x)\ge u\}$ is always one of the $x_j$.

## Key equivalence

For any real $x$ and any $u\in(0,1)$:

$$
F^{-}(u)\le x \iff u\le F(x).
$$

($\Leftarrow$) Suppose $u\le F(x)$. Let $x_k$ be the largest support point with $x_k\le x$. Because $F$ is flat between support points, $F(x_k)=F(x)\ge u$. So $x_k$ is in the set $\{x_j: F(x_j)\ge u\}$, and its minimum satisfies $F^{-}(u)\le x_k\le x$.

($\Rightarrow$) Suppose $F^{-}(u)=x_j\le x$. By definition $F(x_j)\ge u$. Since $F$ is non-decreasing, $F(x)\ge F(x_j)\ge u$.

## Solving the probability

The equivalence turns the two events into the same event:

$$
P\big(F^{-}(U)\le x\big)=P\big(U\le F(x)\big)=F(x),
$$

since $P(U\le a)=a$ for $a\in[0,1]$. So $X=F^{-}(U)$ has CDF $F$.

## Point-probability version

The same idea gives each $p_k$ directly. $F^{-}(u)=x_k$ exactly when $x_k$ is the first support point whose cumulative probability reaches $u$:

$$
F^{-}(u)=x_k \iff F(x_{k-1})<u\le F(x_k).
$$

Therefore

$$
P(X=x_k)=P\big(F(x_{k-1})<U\le F(x_k)\big)=F(x_k)-F(x_{k-1})=p_k.
$$

In other words, $(0,1]$ is cut into consecutive intervals of lengths $p_1,p_2,p_3,\dots$, and $X$ takes the value $x_k$ when $U$ lands in the $k$-th interval.

## Worked example

Take support $x_1,x_2,x_3$ with $p=(0.2,\,0.5,\,0.3)$, so $F=(0.2,\,0.7,\,1)$.

|$U$ falls in|$X$|Probability|
|---|---|---|
|$(0,\,0.2]$|$x_1$|0.2|
|$(0.2,\,0.7]$|$x_2$|0.5|
|$(0.7,\,1]$|$x_3$|0.3|

For example, $u=0.65$ gives $\{x_j: F(x_j)\ge 0.65\}=\{x_2,x_3\}$, whose minimum is $x_2$.

In R, this is:
* `x[findInterval(u, c(0, cumsum(p)), left.open = TRUE)]`, 
or equivalently 
* `x[min(which(cumsum(p) >= u))]`.
