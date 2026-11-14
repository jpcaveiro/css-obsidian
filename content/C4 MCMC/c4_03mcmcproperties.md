# Properties

## Mathematic pillars

MCMC stands for **Monte Carlo** simulation methods via **Markov Chains** (MCMC):

* MCMC is a class of algorithms to simulate complex multivariate distributions. They are based on the construction of a [[homogeneous Markov chain]] whose distribution is the limit of the distribution to be simulated.

![[Pasted image 20260723154120.png]]


## Burn in (or heating)

In Metropolis–Hastings, **burn-in is the initial part of the simulated chain that you discard** before using the remaining states for estimation. Its purpose is to reduce the influence of the starting value $X_0$, which may be far from regions typical of the target distribution $f$. It may take some time for the “walk” to move away from the initial starting point.

For example, suppose you generate $X_1,\ldots,X_{10000}$ and choose a burn-in of $BURN=2000$. You discard the first 2000 states and estimate $E_f[h(X)]$ using the remaining 8000:

$$
\widehat{E_f[h(X)]}
=
\frac{1}{8000}\sum_{t=2001}^{10000} h(X_t)
$$

with $X_t$ drawn from MCMC algorithms.

The intuition is to let the chain approximately “forget” where it started before collecting the states used for inference.

Note that burn-in does not guarantee convergence or make the retained states independent. There is no universally correct burn-in length; trace plots and comparisons between chains started at different points help assess whether initialization effects remain.

After min 14:45 an animation that illustrates this hard problem:
* [Ben Lambert (Oxford)](https://www.youtube.com/watch?v=7H7IvSSty0k&t=1027s)


# MCMC algorithms


![[Pasted image 20260723165541.png]]

Some comments on the text in the image above.

MCMC stands for "Monte Carlo simulation methods via Markov Chains" (MCMC).

A target distribution $f$ is "target" because we want to sample from it, from $f$.

The name "kernel" means "transition kernel" and is a probability distribution from which to make "jumps": given current $X_t$ randomly generate $X_{t+1}$. In Markov chain, a **transition kernel** (often denoted as $K$) represents the **conditional distribution** of the next state in a sequence given its current state. 

A previous note: later the word "proposal" is going also to be need a distribution to propose jumps. However, that proposal (usually named $q$ distribution) is only part of the overall transition kernel of the MCMC.

A transition kernel must obey the property of [[mc_stationary| stationary probability distribution]]: a distribution $f$ is a **stationary probability distribution** for [[mc_kernel|kernel K]] if $X_t \sim f \implies X_{t+1} \sim f$.

By **"build a Markov kernel"** it is meant build an algorithm like Metropolis-Hastings that verifies the basis of MCMC above. As said, this "Markov kernel" depends also on a "proposal distribution" but also on the decision rule to accept or reject a jump.

[[Further reading]]: 

* [[LLM C4 more on Markov kernel]].
* [[LLM C4 ergodic theorem]]

References:

* https://www.publichealth.columbia.edu/research/population-health-methods/markov-chain-monte-carlo
* https://www.stat.purdue.edu/~varao/STAT545/lect17.pdf
* [Ben Lambert (Oxford)](https://www.youtube.com/watch?v=7H7IvSSty0k&t=1027s)