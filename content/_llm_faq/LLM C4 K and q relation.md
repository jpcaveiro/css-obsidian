In the context of the Metropolis-Hastings (M-H) algorithm, the symbols **$K$** and **$q$** represent two different but related levels of probability distributions used to define the movement of the Markov chain.

### **1. Definition of the Symbols**

- **$q(y|x)$ (Candidate or Proponent Distribution):** This is a distribution chosen by the user to **suggest** or propose a new state $y$ given the current state $x$. It is an input to the algorithm.
- **$K(y|x)$ (Transition Kernel):** This represents the **actual** probability (or density) of the Markov chain moving from state $x$ to state $y$. It is the resulting "rule" of the entire M-H process, incorporating both the proposal and the acceptance/rejection decision.

### **2. The Relation Between $K$ and $q$**

The transition kernel $K$ is **constructed** using the candidate distribution $q$. The Metropolis-Hastings algorithm is a method to build a specific Markov kernel that is guaranteed to have the target density $f$ as its **stationary distribution**.

Mathematically, the probability of transitioning from $x$ to a different state $y$ ($y \neq x$) in the kernel $K$ is the product of two events:

1. Proposing the state $y$ using $q(y|x)$.
2. Accepting that proposal with probability $\alpha(x, y)$.

The relation can be expressed as: $$K(y|x) = q(y|x) \cdot \alpha(x, y) \quad \text{for } y \neq x$$ where $\alpha(x, y) = \min\left( \frac{f(y)q(x|y)}{f(x)q(y|x)}, 1 \right)$.

### **3. Key Differences**

- **Role in the Algorithm:** $q$ is the "proposal" mechanism (where you _might_ go), while $K$ is the "realized" transition (where you _actually_ go).
- **Stationarity:** The goal of the M-H algorithm is to ensure that the resulting kernel $K$ satisfies the **stationary distribution equation**: $\int_{\chi} K(y|x)f(x)dx = f(y)$. While $q$ can be almost any irreducible distribution, it does not necessarily have $f$ as its stationary distribution; the acceptance step ($\alpha$) modifies the "raw" proposals of $q$ to ensure the resulting $K$ reaches the correct equilibrium.
- **Symmetry:** $q$ can be **asymmetric** (where $q(y|x) \neq q(x|y)$). In such cases, the M-H algorithm uses the ratio $\frac{q(x|y)}{q(y|x)}$ to correct for this bias within the kernel $K$, ensuring the chain spends the correct amount of time in each region of the target density $f$.