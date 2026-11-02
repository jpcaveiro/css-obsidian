
* ratio f/f
* ratio q/q
* symmetry and asymmetry
* alpha

# ratio f(y)/f(x_t)

In the Metropolis-Hastings (M-H) algorithm, the ratio **$f(y)/f(x_t)$** represents the **relative likelihood** between a proposed candidate state ($y$) and the current state of the chain ($x_t$).

The logic behind this ratio is fundamental to how the algorithm explores a target distribution:

### **1. Independence of Normalizing Constants**

One of the most critical logical advantages of using this ratio is that it allows the simulation of a distribution $f$ even when its **normalizing constant is unknown**. Because the constant would appear in both the numerator ($f(y)$) and the denominator ($f(x_t)$), it cancels out completely, requiring only the functional form of the density to be known.

### **2. Direction and Exploration**

The ratio directs the "movement" of the Markov chain based on the shape of the target density:

- **Moves to Higher Density:** If $f(y) \ge f(x_t)$, the ratio is $\ge 1$. In scenarios with a symmetric proposal distribution (where $q(x|y) = q(y|x)$), this proposed move is **always accepted**. Logically, this encourages the chain to move toward more probable regions of the distribution.
- **Moves to Lower Density:** If $f(y) < f(x_t)$, the ratio is less than 1. The chain does not automatically reject these moves; instead, it accepts them with a probability equal to that ratio. This logic ensures the chain can **explore the entire state space** (irreducibility) and correctly sample from the tails of the distribution rather than simply staying at the peak.

### **3. Maintaining the Stationary Distribution**

This ratio is a core component of the **acceptance probability $\alpha(x_t, y)$**, which is mathematically constructed to ensure that the resulting Markov chain eventually reaches a **stationary distribution** identical to the target density $f$. By balancing the moves according to this ratio, the algorithm guarantees that, in the long run, the time the chain spends in any region is proportional to the density $f$ of that region.

# ratio q/q

In the Metropolis-Hastings algorithm, the addition of the proponent (or candidate) distribution ratio, **$\frac{q(x_t|y)}{q(y|x_t)}$**, to the decision process allows for the use of **asymmetric proposal distributions**.

While the original Metropolis algorithm required the proposal distribution to be symmetric—meaning the probability of proposing a move from $x$ to $y$ was the same as moving from $y$ to $x$—Hastings' generalization expanded the algorithm's flexibility.

### **Why the $q()$ Ratio was Added**
*   **Correcting for Proposal Bias:** If a proposal distribution is asymmetric ($q(x|y) \neq q(y|x)$), the Markov chain would naturally tend to spend more time in regions where the proposal distribution "pushes" it more frequently. Including the $q$ ratio in the acceptance probability $\alpha$ acts as a correction factor that balances this bias, ensuring the chain still converges to the correct **target stationary distribution** $f$.
*   **Broadening Applications:** By accounting for the asymmetry of the proposal, the algorithm can utilize a much wider range of distributions to suggest new states. This is particularly useful in complex multivariate simulations where a symmetric random walk might be inefficient.
*   **Mathematical Consistency:** The full acceptance probability is defined as:
    $$\alpha(x_t, Y) = \min \left( \frac{f(Y)q(x_t|Y)}{f(x_t)q(Y|x_t)}, 1 \right)$$
    This formula ensures that the specific Markov kernel constructed has $f$ as its stationary distribution even when the transition rules ($q$) are not symmetric.

### **Key Consequences**
*   **Independence of $q$ in Symmetric Cases:** If the proponent distribution happens to be symmetric (like a typical Random Walk M-H), the $q$ terms cancel out, and the decision depends solely on the ratio of the target densities: $\frac{f(Y)}{f(x_t)}$.
*   **Normalizing Constants are Unnecessary:** Like the original Metropolis algorithm, this generalized version only depends on the **ratios** of the densities, meaning the normalization constant of the target function $f$ does not need to be known.

# symmetry and asymmetry

No **Metropolis-Hastings**, a condição $q(x|y) = q(y|x)$ significa que a distribuição proposta é **simétrica**.

Isso transforma o algoritmo no **caso especial de Metropolis**, onde a probabilidade de aceitação se simplifica para:

$$
\alpha = \min \left( 1, \frac{\pi(y)}{\pi(x)} \right)
$$

(eliminando o termo $q(y|x)/q(x|y)$).

---
# alpha

In the provided sources, the function **$\alpha(x, y)$** primarily refers to the **Metropolis-Hastings acceptance probability**, which is a core component of the Metropolis-Hastings (M-H) algorithm.

### **Metropolis-Hastings Acceptance Probability**

In the context of Markov Chain Monte Carlo (MCMC) methods, $\alpha$ is used to determine whether the chain should move from its current state to a proposed new state.

- **The Formula:** The general formula for this probability is: $$\alpha(x, y) = \min \left( \frac{f(y)q(x|y)}{f(x)q(y|x)}, 1 \right)$$ In this expression, **$f$** is the **target density** you wish to simulate, and **$q$** is the **candidate (or proponent) distribution** used to suggest a new value $y$ given the current value $x$.
- **The Logic:** One of the main advantages of this algorithm is that it only requires knowledge of the **ratio** of the target densities ($f(y)/f(x)$), meaning the normalization constant of the distribution does not need to be known.
- **Decision Process:** After generating a candidate $y$ from $q(y|x_t)$, a uniform random variable $u$ is drawn from $Unif(0, 1)$. If $u \le \alpha(x_t, y)$, the candidate is **accepted**, and the next state $X_{t+1}$ becomes $y$; otherwise, it is **rejected**, and $X_{t+1}$ remains $x_t$.
- **Symmetric Proponents:** If the proponent distribution is **symmetric** ($q(x|y) = q(y|x)$)—as is the case in a **Random Walk Metropolis-Hastings**—the probability simplifies to: $$\alpha(x_t, y) = \min \left( \frac{f(y)}{f(x_t)}, 1 \right)$$ In this scenario, the acceptance is independent of the proponent distribution $q$.
- **Efficiency:** Monitoring the **acceptance rate** (the percentage of candidates accepted) is a key diagnostic for the algorithm's performance. For one-dimensional cases, a "golden rule" suggests aiming for an acceptance rate of approximately **50%**.

---

### **Other Uses of $\alpha$ in the Sources**

Beyond MCMC, the sources use the symbol $\alpha$ in two other major statistical contexts:

1. **Statistical Significance Level:** In the context of hypothesis testing, $\alpha$ denotes the **significance level**, which represents the maximum allowable probability of a **Type I error** ($P(\text{Reject } H_0 | H_0 \text{ is true}) \le \alpha$). For many practical tests, $\alpha$ is fixed at a standard value like 0.05.
2. **Distributional Parameter:** $\alpha$ frequently serves as a **shape parameter** for various probability distributions mentioned in the text, including the **Beta** distribution, the **Pareto** distribution, and the **Gamma** distribution.