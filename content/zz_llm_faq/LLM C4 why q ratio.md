In the Metropolis-Hastings algorithm, the addition of the proponent (or candidate) distribution ratio, **$\frac{q(x_t|y)}{q(y|x_t)}$**, to the decision process allows for the use of **asymmetric proposal distributions**.

While the original Metropolis algorithm required the proposal distribution to be symmetric—meaning the probability of proposing a move from $x$ to $y$ was the same as moving from $y$ to $x$—Hastings' generalization expanded the algorithm's flexibility.

### **Why the $q()$ Ratio was Added**

- **Correcting for Proposal Bias:** If a proposal distribution is asymmetric ($q(x|y) \neq q(y|x)$), the Markov chain would naturally tend to spend more time in regions where the proposal distribution "pushes" it more frequently. Including the $q$ ratio in the acceptance probability $\alpha$ acts as a correction factor that balances this bias, ensuring the chain still converges to the correct **target stationary distribution** $f$.
- **Broadening Applications:** By accounting for the asymmetry of the proposal, the algorithm can utilize a much wider range of distributions to suggest new states. This is particularly useful in complex multivariate simulations where a symmetric random walk might be inefficient.
- **Mathematical Consistency:** The full acceptance probability is defined as: $$\alpha(x_t, Y) = \min \left( \frac{f(Y)q(x_t|Y)}{f(x_t)q(Y|x_t)}, 1 \right)$$ This formula ensures that the specific Markov kernel constructed has $f$ as its stationary distribution even when the transition rules ($q$) are not symmetric.

### **Key Consequences**

- **Independence of $q$ in Symmetric Cases:** If the proponent distribution happens to be symmetric (like a typical Random Walk M-H), the $q$ terms cancel out, and the decision depends solely on the ratio of the target densities: $\frac{f(Y)}{f(x_t)}$.
- **Normalizing Constants are Unnecessary:** Like the original Metropolis algorithm, this generalized version only depends on the **ratios** of the densities, meaning the normalization constant of the target function $f$ does not need to be known.