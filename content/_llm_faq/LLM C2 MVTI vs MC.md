
# Mean Value Theorem for Integrals and Monte Carlo

* Mean Value Theorem for Integrals (MVTI)

The link between the MVTI and the Monte Carlo method is direct: Monte Carlo is the statistical (and numerical) version of the MVTI, used when the integral is very complicated or has many dimensions.
While the MVTI is deterministic (it guarantees that an exact c exists), Monte Carlo is probabilistic (it estimates the mean value using random samples).

## The Formula That Connects Them

By the MVTI, the mean value of $f$, $\langle f \rangle, on [a; b]$ is:
$\langle f \rangle = \frac{1}{b-a} \int_a^b f(x) dx$
In Monte Carlo, we approximate this mean by the arithmetic mean of ($N$) points drawn at random from the interval:
$$\langle f \rangle \approx \frac{1}{N} \sum_{i=1}^{N} f(x_i), \quad x_i \sim \text{Uniform}(a,b)$$
So the integral is estimated by:
$$\int_a^b f(x) dx \approx \frac{b-a}{N} \sum_{i=1}^{N} f(x_i)$$

Example: $$\int_0^1 x^2 dx$$
Exact value: $1/3 \approx 0.3333$
Monte Carlo with 5 points (randomly drawn x): 0.12; 0.67; 0.45; 0.89; 0.31
$f(x)$: 0.0144 + 0.4489 + 0.2025 + 0.7921 + 0.0961 = 1.554
Estimate = $\frac{1}{5} \times 1.554 = 0.3108$ (error ~6.7%)
With more points (e.g., 10,000), the estimate converges to $0.3333$ by the Law of Large Numbers.

Quick Comparison

| Feature   | MVTI                | Monte Carlo                   |
| --------- | ------------------- | ----------------------------- |
| Nature    | Exact (theoretical) | Approximate (numerical)       |
| Dimension | 1D (or a few)       | High dimensions (10D+, 100D+) |
| Cost      | Low (analytical)    | High (many samples)           |
| Error     | Zero                | Decreases as 1/\sqrt{N}       |

## Why Is Monte Carlo Useful?

Multidimensional integrals: the trapezoidal rule grows as $N^d$, while Monte Carlo scales with $\sqrt{N}$ regardless of dimension.

* Complex functions: no antiderivative, or an irregular domain.
* Physics/Finance: particle simulations, financial options, etc.


See also:
[LLM C2 numeric methods vs Monte Carlo methods](LLM C2 numeric methods vs Monte Carlo methods) (comparison between numerical methods of integration and monte carlo methods of integration)
[chat source](https://chat.deepseek.com/a/chat/s/b6d1e17c-e5d6-400d-8738-d9763aaa1048)