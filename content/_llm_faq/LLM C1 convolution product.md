A **convolution product** is the probability distribution obtained when you add independent random variables. If

$$
S=X_1+\cdots+X_n,
$$

then the distribution of $S$ is called the convolution of the distributions of $X_1,\ldots,X_n$. This is why convolution is central to modelling totals: total demand, aggregate claims, accumulated waiting times, measurement errors, and random-walk positions. Your course notes introduce it precisely in the context of sums of independent random variables. [1]

## Discrete random variables

Let $X$ and $Y$ be independent discrete random variables, with probability mass functions $p_X$ and $p_Y$. For $S=X+Y$,

$$
p_S(s)=P(X+Y=s)
      =\sum_x P(X=x,\;Y=s-x).
$$

Independence gives

$$
\boxed{
p_S(s)=\sum_x p_X(x)\,p_Y(s-x)
}
$$

where the sum only includes values $x$ for which both probabilities are possible.

### Example: two fair dice

Let $X,Y \sim \operatorname{Unif}\{1,\ldots,6\}$, independently. Then $S=X+Y$.

For example,

$$
P(S=7)
=
\sum_x P(X=x)P(Y=7-x).
$$

The valid pairs are

$$
(1,6),(2,5),(3,4),(4,3),(5,2),(6,1),
$$

so

$$
P(S=7)=6\left(\frac16\right)\left(\frac16\right)=\frac16.
$$

For $S=2$, there is only one pair, $(1,1)$, hence

$$
P(S=2)=\frac1{36}.
$$

This produces the familiar triangular distribution for the sum:

$$
P(S=s)=
\begin{cases}
(s-1)/36, & s=2,\ldots,7,\\
(13-s)/36, & s=8,\ldots,12.
\end{cases}
$$

## Continuous random variables

If $X$ and $Y$ are independent continuous variables with densities $f_X$ and $f_Y$, then $S=X+Y$ has density

$$
\boxed{
f_S(s)
=
(f_X*f_Y)(s)
=
\int_{-\infty}^{\infty} f_X(x)\,f_Y(s-x)\,dx
}
$$

The notation $f_X*f_Y$ means “the convolution of $f_X$ and $f_Y$.”

The factor $f_X(x)f_Y(s-x)$ represents the joint density contribution from the combination

$$
X=x,\qquad Y=s-x,
$$

which is exactly the combination needed to make $X+Y=s$. The integral adds the contributions from all such possible decompositions of $s$.

## Important example: normal sums

A major reason convolution matters is that normal distributions are closed under addition. If

$$
X\sim N(\mu_X,\sigma_X^2),
\qquad
Y\sim N(\mu_Y,\sigma_Y^2),
$$

and $X$ and $Y$ are independent, then

$$
\boxed{
X+Y\sim N\!\left(\mu_X+\mu_Y,\;\sigma_X^2+\sigma_Y^2\right)
}
$$

For instance, if

$$
X\sim N(0,1),
\qquad
Y\sim N(3,1),
$$

then

$$
X+Y\sim N(3,2).
$$

More generally, if

$$
Z=aX+bY,
$$

then, under independence,

$$
Z\sim N\!\left(a\mu_X+b\mu_Y,\;a^2\sigma_X^2+b^2\sigma_Y^2\right).
$$

This relates directly to the course example of generating a variable of the form

$$
X=\frac13 X_1+\frac23 X_2,
$$

by independently generating $X_1$ and $X_2$ and then forming their weighted sum. [1]

## Key distinction: convolution vs mixture

These are often confused.

| Construction | How it is formed | Resulting distribution |
|---|---|---|
| **Convolution** | Add random variables, e.g. $S=X+Y$ | Distribution of a total |
| **Mixture** | Choose one of several distributions at random | Weighted average of distributions |

For a two-component mixture, the density may be

$$
f(x)=p f_1(x)+(1-p)f_2(x).
$$

You first choose component 1 with probability $p$, otherwise component 2, and then draw **one** value from the chosen component.

In contrast, for a convolution you generate values from both variables and add them:

$$
S=X+Y.
$$

Your notes present sums/convolution and mixture models consecutively because both combine distributions, but they describe fundamentally different random mechanisms. [1]

## Useful properties

If $X$ and $Y$ are independent and $S=X+Y$, then

$$
E(S)=E(X)+E(Y),
$$

and

$$
\operatorname{Var}(S)=\operatorname{Var}(X)+\operatorname{Var}(Y).
$$

The second identity requires independence; otherwise,

$$
\operatorname{Var}(X+Y)
=
\operatorname{Var}(X)+\operatorname{Var}(Y)
+
2\operatorname{Cov}(X,Y).
$$

Convolution also behaves neatly with transforms:

- **Probability generating functions** multiply for sums of independent nonnegative integer-valued variables.
- **Moment-generating functions** multiply:
  $$
  M_{X+Y}(t)=M_X(t)M_Y(t).
  $$
- **Characteristic functions** multiply:
  $$
  \varphi_{X+Y}(t)=\varphi_X(t)\varphi_Y(t).
  $$

These transform results are often much easier to use than evaluating the convolution sum or integral directly.

## Simulation view

In computational statistics, one often does not calculate the convolution analytically. Instead:

1. Generate $X_1,\ldots,X_n$ independently from their specified distributions.
2. Form the sum
   $$
   S=X_1+\cdots+X_n.
   $$
3. Repeat many times to obtain a sample from the convolution distribution.

That simulation-based interpretation is especially useful when the individual distributions are complicated or the analytic convolution integral has no convenient closed form. [1]

Original:
* https://www.perplexity.ai/search/63fe6055-b12f-46e8-8034-ee54e71ccbaa*