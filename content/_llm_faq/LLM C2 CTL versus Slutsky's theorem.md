
* [[CLT]]
* [[Slutsky theorem]]


The CLT gives you a normal distribution in the limit. Slutsky's theorem doesn't give you any new distribution. It tells you what happens to a limit you already have when you combine it with things that settle down to a constant.

**The CLT** says that for i.i.d. data with finite variance,

$$
\frac{\sqrt n(\bar X_n-\mu)}{\sigma}\xrightarrow{d}N(0,1).
$$

The conditions are on the data, the result is specifically normal, and it needs the true $\sigma$, which is usually unknown.

**Slutsky's theorem** says that if $X_n\xrightarrow{d}X$ and $Y_n\xrightarrow{p}c$, where $c$ is a constant, then:

- $X_n+Y_n\xrightarrow{d}X+c$
- $X_nY_n\xrightarrow{d}cX$
- $X_n/Y_n\xrightarrow{d}X/c$, provided $c\neq 0$

Whatever $X$ is, normal or not, it just gets shifted or scaled.

**They are usually used together.** The CLT gives the $N(0,1)$ limit. The sample standard deviation satisfies $S_n\xrightarrow{p}\sigma$, by the law of large numbers. Slutsky then lets you replace $\sigma$ with $S_n$:

$$
\frac{\sqrt n(\bar X_n-\mu)}{S_n}\xrightarrow{d}N(0,1).
$$

This is what justifies the large-sample confidence interval $\bar X_n \pm z\,S_n/\sqrt n$ and the Monte Carlo error estimates in Chapter 2. Neither theorem gets you there on its own.

A common mistake is forgetting that Slutsky needs $Y_n$ to converge to a constant. It does not work when $Y_n$ converges to a random variable.
