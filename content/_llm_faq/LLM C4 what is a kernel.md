In Markov chains, a **transition kernel** (often denoted as $K$) represents the **conditional distribution** of the next state in a sequence given its current state.

According to the provided sources, here are the key aspects of a kernel in this context:

### **Definition and Function**

- **Next-State Rule:** For a sequence of dependent random variables ${X_t}$, the kernel defines the probability of moving to state $X_{t+1}$ based solely on the current state $X_t$. This is expressed mathematically as $X_{t+1} | X_t, \dots, X_1 \sim K(X_{t+1} | X_t)$.
- **Example (Random Walk):** In a simple random walk where $X_{t+1} = X_t + \epsilon_t$ (with $\epsilon_t \sim N(0, 1)$), the transition kernel corresponds to the probability density function of a normal distribution centered at the current state: $N(X_t, 1)$.

### **Role in MCMC (Markov Chain Monte Carlo)**

The primary goal of MCMC methods is to construct a specific Markov kernel that has a desired **stationary distribution**.

- **Stationary Distribution ($f$):** A distribution $f$ is considered stationary for a kernel $K$ if, when the current state $X_t$ follows $f$, the next state $X_{t+1}$ also follows $f$. This stability is defined by the integral: $$\int_{\chi} K(y|x)f(x)dx = f(y).$$
- **Irreducibility:** A kernel is considered "irreducible" if it allows the sequence to visit any region of the state space, regardless of the starting value $X_0$.
- **Convergence:** In recurrent chains, the stationary distribution $f$ also serves as the **limit distribution**, meaning that as the number of iterations grows, the chain eventually follows the target distribution $f$ regardless of the initial starting point.