

# Metropolis algorithm

First a presentation of the original Metropolis algorithm (without Hastings).

In this chapter the expression **proposal distribution** means the probability of proposing a move from $x$ to $y$. Symbol $q$ is used to indicate a proposal distribution. (The proposal distribution is not, by itself, the transition kernel $K$ stated in previous section but it is part of the transition kernel.)

The original Metropolis algorithm (without Hastings) required a proposal distribution, $q$, to be **symmetric** — meaning the probability of proposing a move from $x$ to $y$ was the same as moving from $y$ to $x$.

The two main inputs of the algorithm are: a target distribution $f$, and proposal distribution $q$:

## target distribution (input f)

* $f$ is the target distribution from which the samples are to be generated.
 
## proposal distribution (input q)

From a "proposal distribution" $q$ given $x_t$ (also called candidate or proponent distribution) one proposes a move $y$:

* given current state, $x_t$, a proposed $y$, to possible give value for the next state $x_{t+1}:=y$, is generated from $Y\sim q|x_t$. An example of a proponent distribution is $q|x_t=N(x_t, 1)$, a symmetrical proposal distribution.

Example of a proposed next state suggested by a random sample from $q|x_t$:

* $x_0 = 1.1$
* $q|x_t=N(x_t,1)$, or $Y\sim N(x_t,1)$
* an instance $y$ is pseudo random number from $N(x_t,1)$, for example, $y=0.1$ but eventually could be negative, like $y=-5$.

Note that $q|x_t$ can be:

* symmetrical (original work of Metropolis et al) where $q(y|x) = q(x|y)$ or 
* asymmetrical (the work of Hastings 2 years later) where $q(y|x) \neq q(x|y)$ to correct possible bias (to be seen in [[c4_05metropolishastings|Metropolis Hastings algorithm]]).


Common examples of **symmetric proposal distributions** (also called candidate or proponent distributions) used in the Metropolis (but also M.-H.) algorithm include:

- **Normal Distribution centered at the current state:** A very common symmetric proposal is $q(y|x) \sim N(x, \sigma^2)$. In this case, the probability of proposing $y$ given $x$ is equal to the probability of proposing $x$ given $y$ because the normal density is symmetric about its mean.
- **Uniform Distribution centered at zero for perturbations:** In a **Random Walk Metropolis-Hastings**, the candidate is generated as $Y_t = X_t + \epsilon_t$, where the perturbation $\epsilon_t$ follows a distribution symmetric about zero. A typical choice is $\epsilon_t \sim Unif(-\delta, \delta)$, where $\delta$ is a parameter that controls the acceptance rate.
- **Student's t-distribution:** Similar to the normal distribution, a t-distribution centered at zero can be used for the random walk perturbation $\epsilon_t$, as it is also symmetric about zero $g(-z) = g(z)$.

## decision rule $\alpha$ 

This decision rule is on work of Metropolis algorithm (before Hastings).

Having inputs $f$ and $q|x_t$ the next step (a new state) depends on:

* $x_t$ is the current state
* $y$ is the proposed next state suggested by a random sample from $q|x_t$

A rule will decide if the state stays in same state $x_{t+1} = x_t$ or $x_{t+1} = y$ (a jump, a transition). Let

$$
\alpha(x_t,y) = \min\left(\frac{f(y)}{f(x_t)},1 \right)
$$

The idea is to compare using a ratio between two densities. Consider the image from [Kapil Sachdeva](https://youtu.be/oX2wIGSn4jY?si=1NmlrEDqVTr0wSFh&t=433) and explanations below:
![[Pasted image 20260723233247.png]]

Suppose:

* white dot is $x_t$; also pay attention to $f(x_t)$ in the blue density;
* orange dot, at right, is the proposal $y$, and $f(y)$ is in the blue density
* (the yellow density is $q|x_t$ where $x_t$ is represented by the white dot.)

In this case, $\alpha(x_t,y)= \min(>1,1)=1$ because $y$ is located in a region of higher density then $x_t$. So the decision is: "move to y". In general rule is:

The Metropolis algorithm decision rule is:

* move to $y$ with probability $\alpha(x_t,y)$  
	* (it is de "direction step" toward more density)
* keep in $x_t$ with probability $1-\alpha(x_t,y)$
	* (it is de "exploratory step" toward lower density but exploring other regions)
* (this decision is done using an independent uniform distribution: 

```
generate u from U(0,1)
if u<alpha
  x(t+1) = y    #move to the proposed position
else
  x(t+1) = x(t) #stays in same position
```


In the situation of the image, the move to $x_{t+1} = y$ is going to occur because proposed $y$ is in a region of higher density. However, sometimes, the reverse happens and $x_{t+1}$ moves away from higher densities.

As a summary, "Direction and Exploration": The ratio directs the "movement" of the Markov chain based on the shape of the target density:

- **Moves to Higher Density:** If $f(y) \ge f(x_t)$, the ratio is $\ge 1$. In scenarios with a symmetric proposal distribution (where $q(x|y) = q(y|x)$), this proposed move is **always accepted**. Logically, this encourages the chain to move toward more probable regions of the distribution.
- **Moves to Lower Density:** If $f(y) < f(x_t)$, the ratio is less than 1. **The chain does not automatically reject these moves**; instead, it accepts them with a probability equal to that ratio. This logic ensures the chain can **explore the entire state space** (irreducibility) and correctly sample from the tails of the distribution rather than simply staying at the peak.

As an example, consider image from [Metropolis–Hastings algorithm - wikipedia](https://en.wikipedia.org/wiki/Metropolis%E2%80%93Hastings_algorithm) that works also for Metropolis only algorithm:

![[Pasted image 20260723234758.png]]

[[Memory is Something We Do]]

Exercise 1. In the above image how many rejections had occurred?

Exercise 2. 

**(a)** [[write R code and run it]], in any computer language, to solve "Exercise 2" of [[_Chapter 4_worksheet_]].

**(b)** [[explain instructions]] in the code.


Reference:
* Metropolis, N., Rosenbluth, A. W., Rosenbluth, M. N., Teller, A. H., & Teller, E. (1953). Equation of State Calculations by Fast Computing Machines. _The Journal of Chemical Physics_, _21_(6), 1087–1092. https://doi.org/10.1063/1.1699114