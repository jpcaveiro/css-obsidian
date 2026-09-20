The **Expectation-Maximization (EM) algorithm** is a deterministic optimization technique designed to calculate **Maximum Likelihood Estimates (MLE)** in scenarios involving unobserved or latent variables. Introduced by Dempster, Laird, and Rubin in 1977, it functions as a **data augmentation method**, where observed data is supplemented with "latent" data to simplify complex likelihood calculations.


Example:
* There are two groups A and B of heights (for example, heights of man and women).
* Z is the random variable that identify the group (A or B)
* Y is the random variable with heights
* **$\theta$**: parameters we want to estimate
	* the means $\mu_A, \mu_B$ and variances $\sigma_A^2, \sigma_B^2$ of the two groups, 
	* and the mixing probability $p$ indicating the proportion of Group A


Step by step:
* $\hat{\theta}^{(i)}$: The current best estimate of those parameters from the previous iteration.


### **1. Core Concept and Notation**
The algorithm distinguishes between two types of variables:
*   $Y$: The vector of **observed variables**:
	* 
*   $Z$: The vector of **non-observed (latent) variables**.
	* Comment: this observed variables will be estimated from current step
*   $\theta$: The parameter to be estimated using the joint distribution of the augmented data $(Y, Z)$.
	* Comment: this parameter will be estimated from current step

The goal is to estimate $\theta$ by maximizing the likelihood of the observed data, $L(\theta | y)$, which is equivalent to the integral of the joint likelihood over the latent space: $L(\theta | y) = \int f(y, z | \theta) dz$.

### **2. Common Applications**
The sources note that EM is particularly useful in structures suggesting:
*   **Missing data**: Where some intended observations were not recorded.
*   **Censored data**: Where the value of a measurement is only partially known.
*   **Mixture of distributions**: Where observations may come from one of several underlying distributions.

### **3. The Algorithm Steps**
The EM algorithm is iterative, starting from an initial estimate $\theta^{(0)}$ and producing a sequence of estimates $\theta^{(i)}$. Each iteration consists of two main steps:

1.  **Expectation Step (E-step):**
This step calculates the expected value of the log-likelihood of the complete sample, conditional on the observed data and the current parameter estimate $\hat{\theta}^{(i)}$. This is represented by the **$Q$ function**:
$$Q(\theta | \hat{\theta}^{(i)}, y) = E_{\hat{\theta}^{(i)}}[\log L_c(\theta | Z, y)]$$
where the expectation is taken with respect to the distribution of $Z$ given $y$ and the current estimate $\hat{\theta}^{(i)}$.

2.  **Maximization Step (M-step):**

This step finds the new parameter estimate $\hat{\theta}^{(i+1)}$ that maximizes the $Q$ function calculated in the E-step:
$$\hat{\theta}^{(i+1)} = \arg \max_{\theta} Q(\theta | \hat{\theta}^{(i)}, y)$$
The process repeats until the estimates converge within a specified precision 
    ($\hat{\theta}^{(i+1)} \approx \hat{\theta}^{(i)}$).

### **4. Key Properties and Limitations**
* **Monotonic Increase**: Using Jensen's inequality, it can be shown that the likelihood of the observed data never decreases between iterations: $L(\hat{\theta}^{(i+1)} | y) \ge L(\hat{\theta}^{(i)} | y)$.
* **Stationary Points**: While the sequence $\hat{\theta}^{(i)}$ generally converges to a stationary point of the likelihood function, it is **not guaranteed to reach the global Maximum Likelihood Estimate** or even a local maximum.
* **Deterministic Nature**: The algorithm is deterministic; starting from the same $\theta^{(0)}$ will always yield the same result.
* **Practical Implementation**: Because the likelihood surface can be "meandering" with several local maxima, it is a common practice to run the EM algorithm from **several randomly chosen starting points** to increase the chance of finding the global maximum.

