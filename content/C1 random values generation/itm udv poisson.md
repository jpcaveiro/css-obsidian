# inverse transform method for Poisson

Keywords:

* [[univariate discrete variables]]
* [[Poisson distribution]]


Consider the Poisson distribution
![[Poisson distribution]]

As it can be seen in the general case of [[itm udv|Inverse transform method for univariate discrete variables]], the importance of having all distinct probabilities $p_i=P(X=i)$ is necessary to calculate $F^{-1}(u)$.

However, sometimes it is important to speed up algorithms: this one depends on $i$ factorial.  Calculating $i!$ could be a computational slow procedure.  To overcome the possible slow speed one can deduce a recursive relation for $p_{i+1} =P(X=i+1)$ as a function of $p_i=P(X=i)$.

The relation $p_{i+1} = \frac{\lambda}{i+1} p_i$ can be written for the Poisson mass probability function. This is explored in the following exercises:

[[Memory is Something We Do]]

Exercise 1. Considering the Poisson probability mass function, [[deduce]] a recursive relation for $p_{i+1} =P(X=i+1)$ as a function of $p_i=P(X=i)$.
> [!example]- solution
> * use pmf of Poisson
> * $p_0 = e^{-\lambda}$
> * $p_{i+1} = \frac{\lambda}{i+1} p_i$ for $i=0,\ldots$

Exercise 2. Use [[itm udv|the discrete case]] to [[write pseudo code]] for a random generator for a Poisson variable.
> [!example]- solution
> general scheme
> ```
>   if         u <= p0 then return 0
>   if    p0 < u <= p0+p1 then return 1
>   if p0+p1 < u <= p0+p1+p2 then return 2
>   etc
> ```
> 
> ```
> p0 = exp(-lambda)
> p = p0    #current p_i
> psum = p0 #sum p0+p1+...p_current
> u = generate from U(0;1)
> i = 0
> while u > psum  #search
>      i = i + 1  #try next i
>      p = p * lambda/i  #now i is i+1
>      psum = psum + p
>  return i #generated value
> ```
> ![[Pasted image 20260623011618.png]]

Exercise 3. [[run R code]] of the example and check results.
> [!example]- proposal
> ![[Pasted image 20260623011724.png]]
