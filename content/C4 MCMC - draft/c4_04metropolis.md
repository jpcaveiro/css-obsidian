MCMC is "Monte Carlo simulation methods via Markov Chains" (MCMC)

![[Pasted image 20260723165541.png]]

Comments:

1. A target distribution $f$ is "target" because we want to sample from it, from $f$.
2. The name "kernel" means "transition kernel" and is a probability distribution to do "jumps": a distribution that generate a jump from $X_t$ to $X_{t+1}$.
	1. In Markov chains, a **transition kernel** (often denoted as $K$) represents the **conditional distribution** of the next state in a sequence given its current state.
	2. More in [[LLM C4 what is a kernel]].
3. A transition kernel must obey the property of [[mc_stationary| stationary probability distribution]]: 
	* A distribution $f$ is a **stationary probability distribution** for [[mc_kernel|kernel K]] if $X_t \sim f \implies X_{t+1} \sim f$.
4. By "build a Markov kernel" it is meant, by now, the algorithm Metropolis-Hastings that will follow in next section.
5. [[to do]] "the integrals are approximated by the Ergodic Theorem".

# Metropolis algorithm

The original Metropolis algorithm (without Hastings) required a proposal distribution, $q$, to be symmetric—meaning the probability of proposing a move from $x$ to $y$ was the same as moving from $y$ to $x$.

The two main inputs are: target distribution $f$, and proposal distribution $q$.
### target distribution (input f)

* $f$ is the target distribution from which the samples are to be generated
### proposal distribution (input q)

In what follow, $K$ (transition kernel) and $q$ (proposal distribution) are intrinsic related but not the same, as we will see.

$q|x_t$ is the "proposal distribution" (also called candidate or proponent distribution) used in the Metropolis (and later in Hastings):
* given current state, $x_t$, a proposed $y$, to possible give value for the next state $x_{t+1}$, is generated from $Y\sim q|x_t$. As an example of a proponent distribution: $q|x_t=N(x_t, 1)$ (example of a symmetrical proposal distribution)

Example of a proposed next state suggested by a random sample from $q|x_t$:
* $x_0 = 1.1$
* $q|x_t=N(x_t,1)$, or $Y=N(x_t,1)$
* $y$ is an instance PRN from Y like $y=0.1$ but eventually could be larger like $y=-5$.

Note that $q|x_t$ can be:
	* symmetrical (original work of Metropolis et al) where $q(y|x) = q(x|y)$ or 
	* asymmetrical (the work of Hastings 2 years later) where $q(y|x) \neq q(x|y)$ to correct possible bias (to be seen in [[c4_05metropolishastings]]).

Common examples of **symmetric proposal distributions** (also called candidate or proponent distributions) used in the Metropolis(-Hastings) algorithm include:

- **Normal Distribution centered at the current state:** A very common symmetric proposal is $q(y|x) \sim N(x, \sigma^2)$. In this case, the probability of proposing $y$ given $x$ is equal to the probability of proposing $x$ given $y$ because the normal density is symmetric about its mean.
- **Uniform Distribution centered at zero for perturbations:** In a **Random Walk Metropolis-Hastings**, the candidate is generated as $Y_t = X_t + \epsilon_t$, where the perturbation $\epsilon_t$ follows a distribution symmetric about zero. A typical choice is $\epsilon_t \sim Unif(-\delta, \delta)$, where $\delta$ is a parameter that controls the acceptance rate.
- **Student's t-distribution:** Similar to the normal distribution, a t-distribution centered at zero can be used for the random walk perturbation $\epsilon_t$, as it is also symmetric about zero $g(-z) = g(z)$.

[[Memory is Something We Do]]
* [[Ex 4-q-01]] (talvez passar o texto abaixo para o exercício)


### decision rule $\alpha$ (Metropolis algorithm)

Having inputs $f$ and $q|x_t$ the next step (a new state) depends on:
* $x_t$ is the current state
* $y$ is the proposed next state suggested by a random sample from $q|x_t$

A rule will decide if the state stays in same state $x_{t+1} = x_t$ or $x_{t+1} = y$ (a jump, a transition). Let
$$
\alpha(x_t,y) = \min\left(\frac{f(y)}{f(x_t)},1 \right)
$$
The idea is to compare using a ratio between two densities. Consider the image from [# Metropolis-Hastings - VISUALLY EXPLAINED!](https://youtu.be/oX2wIGSn4jY?si=1NmlrEDqVTr0wSFh&t=433)
![[Pasted image 20260723233247.png]]

Suppose:
* white dot is $x_t$, and also consider $f(x_t)$ in the blue density
* orange dot, at right, is the proposal $y$, and $f(y)$ is in the blue density
* (the yellow density is $q|x_t$ where $x_t$ is represented by the white dot.)

In this case, $\alpha(x_t,y)= \min(>1,1)=1$ because $y$ is located in a region of higher density then $x_t$. So the decision is: "move to y". In general rule is:

The Metropolis algorithm decision rule is:
* move to $y$ with probability $\alpha(x_t,y)$  
	* (it is de "direction step" toward more density)
* keep in $x_t$ with probability $1-\alpha(x_t,y)$
	* (it is de "exploratory step" toward lower density but exploring other regions)
* (this decision is done using a uniform distribution)


In the situation of the image, the move to $x_{t+1} = y$ is going to occur because proposed $y$ is in a region of higher density. However, sometimes, the reverse happens and $x_{t+1}$ moves away from higher densities.

As a summary, "Direction and Exploration": The ratio directs the "movement" of the Markov chain based on the shape of the target density:
- **Moves to Higher Density:** If $f(y) \ge f(x_t)$, the ratio is $\ge 1$. In scenarios with a symmetric proposal distribution (where $q(x|y) = q(y|x)$), this proposed move is **always accepted**. Logically, this encourages the chain to move toward more probable regions of the distribution.
- **Moves to Lower Density:** If $f(y) < f(x_t)$, the ratio is less than 1. The chain does not automatically reject these moves; instead, it accepts them with a probability equal to that ratio. This logic ensures the chain can **explore the entire state space** (irreducibility) and correctly sample from the tails of the distribution rather than simply staying at the peak.

As an example, consider image from [Metropolis–Hastings algorithm - wikipedia](https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm):

![[Pasted image 20260723234758.png]]

[[to do]] melhorar a imagem ao cenário deste texto

[[Further Reading]]
* [[LLM C4 K and q relation]]
* [[LLM C4 why q ratio]]
* [[LLM C4 what is alpha]]
to explain why Hastings (2 years later) proposed a new decision rule $\alpha$:
$$
\alpha(x_t,y) = \min\left(\frac{f(y)}{f(x_t)} \frac{q(x_y|y)}{q(y|x_t)},1 \right)$$

Next, reading is [[c4_05metropolishastings]].