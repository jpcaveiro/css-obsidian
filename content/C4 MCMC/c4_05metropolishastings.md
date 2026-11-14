# Metropolis-Hastings algorithm

 In complex **multivariate models**, simple **symmetric** random walks can be quite inefficient. In these cases, **asymmetric proposal** distributions are designed to "push" the chain more effectively toward high-probability regions or along specific correlation structures . By utilizing non-symmetric transition rules that favor movement in certain directions, the algorithm can explore high-dimensional spaces more efficiently than a standard symmetric proposal .

An asymmetric proposal means $q(x|y) \neq q(y|x)$, in general and Metropolis-Hastings incorporates a ratio of proposals using $q(y|x)$ and $q(x|y)$  in the decision function $\alpha(x,y)$:

![[Pasted image 20260724002946.png]]

Before a detailed explanation watch a [video simulation step by step](https://www.youtube.com/watch?v=AttRPX-kyrs) and the purpose.

In Metropolis–Hastings, the $f$-ratio accounts for the target distribution, while the $q$-ratio corrects the proposal's directional bias. Together, they balance moves between states so that $f$ is a stationary distribution of the chain.

In what follows consider:

* forward proposal is a move $x \to y$ 
* reverse proposal is a move $y\to x$

(Note: reverse and forward has nothing to do with XX axis and a new step proposal $y$  can be at right of $x$ $x <y$ or, otherwise $x>y$.)

For current state $x$ and proposed state $y$, the acceptance rule is:

$$
\alpha(x,y)=
\min\left\{1,\;
\underbrace{\frac{f(y)}{f(x)}}_{\text{target ratio}}
\underbrace{\frac{q(x\mid y)}{q(y\mid x)}}_{\text{proposal correction}}
\right\}.
$$


- Target ratio $f(y)/f(x)$: compares how much density the target assigns to $y$ versus $x$; by itself, it favors moves toward higher target density.
- Proposal ratio $q(x\mid y)\,/\,q(y\mid x)$: compares the reverse proposal, a move $y\to x$, with the forward proposal, a move $x \to y$; if proposing $x\to y$ is easier than proposing $y\to x$, this factor reduces acceptance of the forward move to compensate.

Why multiply them?

The key is to compare **flows**, not just target densities. The proposed flow from $x$ to $y$ combines how often we are at $x$, represented by $f(x)$, with how readily we propose $y$, represented by $q(y\mid x)$.

Thus the two proposed flows are

$$
\underbrace{f(x)q(y\mid x)}_{\text{forward flow}},
\qquad
\underbrace{f(y)q(x\mid y)}_{\text{reverse flow}}.
$$

Acceptance must balance those flows, giving the detailed-balance condition:

$$
f(x)q(y\mid x)\alpha(x,y)
=
f(y)q(x\mid y)\alpha(y,x).
$$
![[Pasted image 20261111141357.png]]


The ratio that matters is therefore simply **reverse proposed flow divided by forward proposed flow**:

$$
\frac{\text{reverse flow}}{\text{forward flow}}
=
\frac{f(y)q(x\mid y)}{f(x)q(y\mid x)}
=
\frac{f(y)}{f(x)}
\frac{q(x\mid y)}{q(y\mid x)}.
$$

**A small example**. Suppose two states should be equally frequent, $f(x)=f(y)$.

But the proposal probabilities are not symmetrical:

* $q(y\mid x)=0.8$ (probability of a jump from $x$ to $y$), and 
* $q(x\mid y)=0.2$ (probability of a jump from $y$ to $x$).

Using only $f(y)/f(x)=1$ would accept every proposal, even though proposals favor $x\to y$ four times as strongly. The correction gives

$$
\alpha(x,y)=\min\{\frac{f(x)}{f(y)}\,\frac{0.2}{0.8},1\}=1 \times 0.25 = 0.25,
\qquad
\alpha(y,x)=\min\{\frac{f(y)}{f(x)}\,\frac{0.8}{0.2},1\} = 1.
$$

Consequently, the actual move probabilities are equal:

$$
P(x\to y)=0.8 \times 0.25=0.2,
\qquad
P(y\to x)=0.2 \times 1=0.2.
$$
recalling that a move is proposed with $q(y,x)$ and the jump is done with probability $\alpha(x,y)$, and vice versa.

That is the purpose of $q/q$ is to **remove the imbalance** introduced by the proposal, without removing the preferences specified by $f$. When the proposal is symmetric, $q(y\mid x)=q(x\mid y)$, that correction is $1$, leaving only the usual Metropolis target ratio.


[[Memory is Something We Do]]

Exercise. The target distribution  $f$ of the next exercise is is called [[Rayleigh distribution]].
![[Pasted image 20260724003343.png]]
**(c)** [[explain instructions|Explain, with detail, all R instructions]].

> [!example]- solution
> (a) 
> ![[Pasted image 20260724003423.png]]
> ![[Pasted image 20260724003437.png]]
> ![[Pasted image 20260724003449.png]]
> ![[Pasted image 20260724003504.png]]
> 


![[Pasted image 20260724003529.png]]
Recall [[c4_03mcmcproperties|Burn in (or heating)]] concept and a suggested solution.


The following video sumarizes all this steps: [DataMListic](https://www.youtube.com/watch?v=7IpvsfRgTTY).

Reference:

* Hastings, W. K. (1970). Monte Carlo sampling methods using Markov chains and their applications. _Biometrika_, _57_(1), 97–109. https://doi.org/10.1093/biomet/57.1.97
* https://www.mirkoklukas.com/blog/metropolis-hastings.html

# Independent Metropolis-Hastings algorithm

![[Pasted image 20261109161118.png]]

**Independent Metropolis–Hastings**, also called the independence sampler, is a special case of MH in which every candidate is drawn from the same **fixed proposal distribution**, independently of the current state: $q(y\mid x)=q(y)$. 

The crucial distinction is that **the proposals are independent, but the resulting chain states generally are not**. Rejection makes the next state equal to the current state, so the output is still a Markov chain rather than an independent sample.

**When does it work well?**

The **efficiency** of this method depends on the proposal distribution $q$ being close to $f$.

A good $q$ approximates the whole target $f$ while avoiding regions where $f/q$ becomes excessively large. A particularly useful theoretical condition is $f(z)\leq Mq(z)$ for some finite $M$, which gives uniform ergodicity; a poor proposal can instead produce long periods of repeated states.

In the ideal case $q=f$, every candidate is accepted and the output is genuinely independent draws from $f$. In general, remember: **independence describes the proposal mechanism, not the output sample**.


[[Memory is Something We Do]]

Example if MH with **independent** proposal $Y\sim U(0;1)$. Notice that [[beta distribution]] lives in interval $[0; 1]$.

![[Pasted image 20260724003030.png]]

> [!example]- solution
> ![[Pasted image 20260724003048.png]]
> ![[Pasted image 20260724003104.png]]
> ![[Pasted image 20260724003114.png]]
> ![[Pasted image 20260724003123.png]]
> ![[Pasted image 20260724003135.png]]
> 


Reference:

* Holden, L., Hauge, R., & Holden, M. (2009). Adaptive independent Metropolis–Hastings. The Annals of Applied Probability, 19(1), 395–413. [https://doi.org/10.1214/08-AAP545](https://doi.org/10.1214/08-AAP545).


# Metropolis-Hastings with Random Walk


![[Pasted image 20260724003601.png]]


Common choices for $g$

| $g$                 | Density $g(z)$                                          | Proposal $q(y\|x)$        | Notes                                                                |
| ------------------- | ------------------------------------------------------- | ------------------------- | -------------------------------------------------------------------- |
| Normal              | $\frac{1}{\sigma\sqrt{2\pi}}e^{-z^2/2\sigma^2}$         | $N(x,\sigma^2)$           | Default choice; tune $\sigma$                                        |
| Uniform             | $\frac{1}{2\delta}\mathbf 1\{\lvert z\rvert\le\delta\}$ | $U(x-\delta,\,x+\delta)$  | Steps are bounded by $\delta$                                        |
| Student t           | $t_\nu$ scaled by $s$                                   | $x + s\,T_\nu$            | Heavier tails, so it sometimes makes big jumps                       |
| Laplace             | $\frac{1}{2b}e^{-\lvert z\rvert/b}$                     | $x + \text{Laplace}(0,b)$ | Sharp peak at 0, heavier tails than the normal                       |
| Cauchy              | $\frac{1}{\pi s(1+(z/s)^2)}$                            | $x + s\,C$                | Very heavy tails; useful for multimodal targets                      |
| Multiv. normal | $N_d(\mathbf 0,\Sigma)$                                 | $N_d(\mathbf x,\Sigma)$   | In $d$ dimensions; often $\Sigma \approx \frac{2.38^2}{d}\,\Sigma_f$ |

 Requirements on $g$

- **It must be a density** on step sizes. It does not need to look anything like $f$.
- **It must be positive in a neighbourhood of 0.** This lets the chain reach every region where $f > 0$ (irreducibility).
- **Symmetry is optional.** If $g$ is skewed, the method is still valid, but the ratio no longer cancels:

$$
\alpha = \min\!\left(1,\ \frac{f(y)}{f(x)}\cdot\frac{g(x-y)}{g(y-x)}\right).
$$



![[Pasted image 20260724003614.png]]

* (The slide mixes indices slightly; with $Y_t=X_{t-1}+\varepsilon_t$, the acceptance probability should be written $\alpha(X_{t-1},Y_t)$, not $\alpha(X_t,Y_t)$.)


![[Pasted image 20260724003624.png]]


The blue part in slide describes how to build a Markov chain whose stationary distribution is $N(0;1)$. If the current state is $X_{t-1}=x$, propose

$$
Y_t=x+\varepsilon_t.
$$

Choose the noise independently of the current state, with a density $g$ symmetric about zero. For example, we could use $\varepsilon_t\sim N(0,\sigma^2)$ or $\varepsilon_t\sim U(-\delta,\delta)$.

Our target density is

$$
f(x)=\frac{1}{\sqrt{2\pi}}\exp\!\left(-\frac{x^2}{2}\right).
$$

For a symmetric proposal, the acceptance probability is

$$
\alpha(x,y)=\min\left\{1,\frac{f(y)}{f(x)}\right\}.
$$

Substituting the normal density gives

$$
\frac{f(y)}{f(x)}
=
\frac{\cancel{1/\sqrt{2\pi}}\,e^{-y^2/2}}
     {\cancel{1/\sqrt{2\pi}}\,e^{-x^2/2}}
=
e^{(x^2-y^2)/2}.
$$

Hence the slide’s formula:

$$
\alpha(x,y)=\min\left\{1,\exp\!\left(\frac{x^2-y^2}{2}\right)\right\}.
$$

Notice that this exponential comes from the **target density `f`**, not from the noise density $g$.

**What the rule means?**

The standard normal density is highest at zero and decreases as the distance from zero increases. Thus the acceptance decision compares $|y|$ with $|x|$:

- Closer to zero, $|y|\le |x|$: then $x^2-y^2\ge0$, so $\alpha(x,y)=1$. Always accept.
- Farther from zero, $|y|>|x|$: then $x^2-y^2<0$, so $\alpha(x,y)<1$. Accept with that probability.

For example, from $x=1$, a proposal $y=0.5$ is always accepted. A proposal $y=2$ is accepted with probability

$$
\alpha(1,2)=e^{(1-4)/2}=e^{-1.5}\approx0.223.
$$

Draw $U_t\sim U(0,1)$, independently, and set

$$
X_t=
\begin{cases}
Y_t,&U_t\le\alpha(X_{t-1},Y_t),\\
X_{t-1},&\text{otherwise}.
\end{cases}
$$

The proposal $Y_t$ is therefore not automatically the next state: rejection means repeating the current value.

# Metropolis-Hastings when proposal is symmetric

This slide theme is presented as [[c4_04metropolis|Metropolis algorithm]]:

![[Pasted image 20261109163434.png]]



[[Further reading]]

* [[LLM C4 why q ratio]] to explain why Hastings (2 years later) proposed a new decision rule $\alpha$:

$$
\alpha(x_t,y) = \min\left(\frac{f(y)}{f(x_t)} \frac{q(x_y|y)}{q(y|x_t)},1 \right)$$


* [[LLM C4 K and q relation]] (Markov kernel $K$ and proposal function $q$ are related but $q$ is not a kernel)
* [[LLM C4 what is alpha]] (revision of concepts)


