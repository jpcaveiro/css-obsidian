
Summary.
1. Slutsky's theorem says you can treat a term that converges in probability to a constant as that constant when doing arithmetic with a term that converges in distribution — making it the workhorse behind studentization and consistent-estimator substitution in asymptotic inference.
2. The requirement that $Y_n$ converges to a constant is important.
3. A common compact form: if $A_n \xrightarrow{p} a$, $B_n \xrightarrow{p} b$, and $X_n \xrightarrow{d} X$, then $A_n X_n + B_n \xrightarrow{d} aX + b$. (https://www.stat.washington.edu/jaw/COURSES/580s/581/LECTNOTES/ch2.pdf)

## Slutsky's Theorem

Slutsky's theorem (often spelled "Slutzky") is a foundational result in asymptotic theory that extends the usual algebra of limits to sequences of random variables. In short, it lets you combine a sequence converging **in distribution** with a sequence converging **in probability to a constant** as if the constant were just an ordinary number.[[en.wikipedia](https://en.wikipedia.org/wiki/Slutsky's_theorem)]

### Statement

Let $X_n$ and $Y_n$ be sequences of random variables (or vectors/matrices). If

$$
X_n \xrightarrow{d} X \quad\text{and}\quad Y_n \xrightarrow{p} c
$$

where $c$ is a constant, then: (https://pages.stat.wisc.edu/~shao/stat609/stat609-21.pdf)

- **Addition:** $X_n + Y_n \xrightarrow{d} X + c$
- **Multiplication:** $X_n Y_n \xrightarrow{d} cX$
- **Division:** $X_n / Y_n \xrightarrow{d} X/c$, provided $c \neq 0$

A common compact form.
If 
$$A_n \xrightarrow{p} a, \quad B_n \xrightarrow{p} b,\quad \text{ and } \quad X_n \xrightarrow{d} X,$$then
$$A_n X_n + B_n \xrightarrow{d} aX + b.$$
### Why it works

The key fact is that convergence in probability to a constant is "rigid": if $Y_n \xrightarrow{p} c$, then the joint vector $(X_n, Y_n)$ converges in distribution to $(X, c)$. Applying the **continuous mapping theorem** to the functions $g(x,y) = x+y$, $xy$, and $x/y$ then yields the three results above.
### Crucial caveat

The second sequence must converge to a **constant**, not to a random variable. If both $X_n \xrightarrow{d} X$ and $Y_n \xrightarrow{d} Y$ (with $Y$ random), their marginals alone are **not** enough — you need joint convergence.

### Why it matters in statistics

The theorem's main practical role is justifying the **"plug-in" principle**: replacing unknown parameters with consistent estimators inside asymptotic distributions.

The canonical example is the **studentized sample mean**. By the CLT,

$$
\frac{\bar X_n - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} N(0,1).
$$

In practice $\sigma$ is unknown, so we use a consistent estimator $\hat\sigma_n \xrightarrow{p} \sigma$. Since $\hat\sigma_n/\sigma \xrightarrow{p} 1$, Slutsky's theorem gives

$$
\frac{\bar X_n - \mu}{\hat\sigma_n/\sqrt{n}} \xrightarrow{d} N(0,1),
$$
which underpins t-statistics, confidence intervals, and hypothesis tests under large-sample approximations.


## References

* https://en.wikipedia.org/wiki/Slutsky's_theorem
* https://www.stat.washington.edu/jaw/COURSES/580s/581/LECTNOTES/ch2.pdf
* [statlect](https://www.statlect.com/asymptotic-theory/Slutsky-theorem)
* [web.mit](https://web.mit.edu/14.383/www/14-383-1-2.pdf)
* [people.stat.sc](https://people.stat.sc.edu/gregorkb/STAT_712_fa_2022/STAT_712_Lec_15_slides.pdf)