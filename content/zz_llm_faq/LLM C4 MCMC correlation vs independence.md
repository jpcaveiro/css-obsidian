
Question: MCMC produces correlated variables. Why can they be used in producing independent random outcomes? 

The short answer: this touches the exact point where MCMC differs from everything in Chapters 1–3. MCMC samples are never independent, and that's fine — the guarantees you need don't require independence. Here's the breakdown.

## Two different properties

There are two separate claims that are easy to conflate:

1. **Marginal correctness** — each individual $X_t$ is a valid draw from the target $f$.
2. **Independence** — the joint distribution of $(X_1, X_2, \ldots)$ factorizes.

MCMC only ever promises (1). As in section [[c4_04metropolis]] notes state, the acceptance rule $\alpha$ is built so that $f$ is a **stationary distribution** for the kernel: if $X_t \sim f$, then $X_{t+1} \sim f$. Correlation is a property of the _joint_ distribution — it changes how consecutive values move together, not what each value's marginal distribution is. So a chain can be heavily autocorrelated and still have every single state marginally distributed as $f$. For example, the random-walk proposal in your notes, $q|x_t = N(x_t,1)$, guarantees correlation by construction (each state is centered on the previous one), and that's not a bug.

## Why estimates still work

The reason you can compute means, probabilities, and integrals from correlated samples is the **Ergodic Theorem**. Under mild conditions (irreducibility, aperiodicity, stationarity), the Markov chain version of the law of large numbers holds:

$$
\frac{1}{n}\sum_{t=1}^{n} h(X_t) \;\xrightarrow{\text{a.s.}}\; \mathbb{E}_f[h(X)]
$$

even though the $X_t$ are dependent. The [[LLM C2 law of large numbers]] doesn't need independence — that's a sufficient condition for [[iid]] sampling, not a requirement. So the histogram of chain values converges to $f$, and averages converge to expectations.

## What correlation actually costs

It doesn't break correctness; it breaks **efficiency**. With autocorrelation $\rho_k$, the variance of your estimator is inflated by a factor:

$$
\text{Var}(\hat\mu) \approx \frac{\sigma^2}{n}\left(1 + 2\sum_{k=1}^{\infty}\rho_k\right)
$$

The term in parentheses converts your $n$ iterations into an **effective sample size** (ESS) smaller than $n$. A chain with strong positive autocorrelation might give ESS $\approx n/10$: you have 10,000 draws but the precision of only ~1,000 iid samples. Two practical consequences:

- Standard error formulas from Chapter 2 (which assume iid) **underestimate** the true Monte Carlo error.
- The fix is simply running the chain longer — not fixing the correlation itself.

## Where it does need care

- **Burn-in**: early states depend on $x_0$ and aren't yet distributed as $f$; discard them.
- **Proposal tuning**: in random-walk Metropolis there's a real trade-off — small $\sigma$ gives high acceptance but the chain crawls (high autocorrelation); large $\sigma$ causes many rejections, so the chain repeats values (also autocorrelation). The usual targets are acceptance rates around 0.44 in one dimension and ~0.234 in higher dimensions.
- **Thinning** (keeping every $k$-th value) reduces autocorrelation between kept samples, but it mostly throws away information; running longer is usually better.
- **Diagnostics**: trace plots and autocorrelation plots tell you how bad it is; if the trace looks like a slow wandering band, ESS is low.

## The trade-off in one sentence

Chapter 1 methods (inverse transform, rejection) give you genuinely [[iid]] samples, but only work when you can sample $f$ directly; MCMC gives up independence in exchange for the ability to sample virtually any $f$ — as your notes put it, "a class of algorithms to simulate complex multivariate distributions." Independence is the price, not a requirement.

