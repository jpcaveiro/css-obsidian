Here’s a simple example of an **envelope** in the rejection method for generating random values.

Suppose we want to generate random samples from the density:

$$
f(x) = 6x(1-x), \quad 0 \le x \le 1
$$

This is the density of a Beta distribution with parameters 2 and 2.

## Step 1: Choose an envelope distribution

Use the uniform distribution on the interval from 0 to 1:

$$
g(x) = 1, \quad 0 \le x \le 1
$$

We need a constant such that:

$$
f(x) \le M g(x)
$$

for all values of x.

Since:

$$
f(x) = 6x(1-x)
$$

has its maximum at:

$$
x = 0.5
$$

we get:

$$
f(0.5) = 6(0.5)(0.5) = 1.5
$$

So we can use:

$$
M = 1.5
$$

The envelope is therefore:

$$
Mg(x) = 1.5
$$

This horizontal line sits above the target density everywhere on the interval from 0 to 1.

## Step 2: Rejection sampling rule

1. Generate a candidate value:

$$
X \sim \text{Uniform}(0,1)
$$

2. Generate another random value:

$$
U \sim \text{Uniform}(0,1)
$$

3. Accept X if:

$$
U \le \frac{f(X)}{Mg(X)}
$$

In this example:

$$
\frac{f(X)}{Mg(X)} = \frac{6X(1-X)}{1.5} = 4X(1-X)
$$

So the acceptance rule becomes:

$$
U \le 4X(1-X)
$$

## Python example

```python
import random
import matplotlib.pyplot as plt

def sample_beta_2_2(n: int) -> list[float]:
    if n <= 0:
        raise ValueError("n must be positive")

    samples = []

    while len(samples) < n:
        # Candidate from Uniform(0, 1)
        x = random.random()

        # Uniform value for acceptance test
        u = random.random()

        # Acceptance probability
        accept_prob = 4 * x * (1 - x)

        if u <= accept_prob:
            samples.append(x)

    return samples


# Generate samples
samples = sample_beta_2_2(10_000)

# Plot histogram
plt.hist(samples, bins=40, density=True, alpha=0.7, label="Generated samples")

# Plot target density
xs = [i / 1000 for i in range(1001)]
fx = [6 * x * (1 - x) for x in xs]

plt.plot(xs, fx, "r", linewidth=2, label="Target density")
plt.legend()
plt.xlabel("x")
plt.ylabel("Density")
plt.show()
```

## Interpretation

The uniform distribution acts as the **proposal distribution**.

The constant-height curve:

$$
Mg(x) = 1.5
$$

is the **envelope**.

Random points are generated under this envelope. If a point falls under the target density curve, we accept it. Otherwise, we reject it. Over many samples, the accepted values follow the desired target distribution.