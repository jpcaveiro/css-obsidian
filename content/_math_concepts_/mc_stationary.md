
[[definition]] stationary probability distribution $f$
A distribution $f$ is a **stationary probability distribution** for [[mc_kernel|kernel $K$]] if:

$$X_t \sim f \implies X_{t+1} \sim f$$

Formally, this stability condition is expressed by:

$$\int_{\chi} K(y \mid x)\, f(x)\, dx = f(y)$$

where $\chi$ is the **state space** — the set of all possible values the chain can visit.

In words: if the chain is currently distributed according to $f$, applying the kernel $K$ leaves the distribution unchanged. The chain is then said to be *at stationarity*.

[[math result]] Convergence property:

In recurrent (irreducible) chains, $f$ is also the **limit distribution**: regardless of the starting point $X_0$, the chain eventually distributes according to $f$ as the number of iterations grows. This is the key property exploited by MCMC methods.
