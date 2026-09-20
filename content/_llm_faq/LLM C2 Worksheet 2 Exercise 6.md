

Based on the problem statement, here is the step-by-step solution. The problem requires using Monte Carlo simulation to verify the properties of a hypothesis test for variance and to construct a confidence interval.

### **Problem Setup and Assumptions**
*   **Null Hypothesis ($H_0$):** $\sigma^2 = 4$
*   **Alternative Hypothesis ($H_1$):** $\sigma^2 > 4$ (Right-tailed test)
*   **Significance Level:** $\alpha = 0.05$
*   **Sample Size:** $n = 100$
*   **Distribution:** Normal with unit mean ($\mu = 1$).
*   **Number of Replicates:** 10,000.
*   *Implicit Assumption:* To estimate the Type I error rate $\alpha$ in part (a), the Monte Carlo simulation must generate data under the null hypothesis. Therefore, we simulate from $N(\mu=1, \sigma^2=4)$.

---

### **Part (a): Estimating $\alpha$ via Monte Carlo**

**1. Theoretical Background**
The test statistic for a hypothesis test about a population variance (when the population is normal) is:
$$T = \frac{(n-1)S^2}{\sigma_0^2}$$
Under $H_0$, $T$ follows a chi-square distribution with $n-1$ degrees of freedom: $T \sim \chi^2_{n-1}$.
For $n=100$, $df = 99$. We reject $H_0$ if $T > \chi^2_{1-\alpha, 99}$.
Using a chi-square table or software, the critical value is:
$$\chi^2_{0.95, 99} \approx 123.225$$

**2. Monte Carlo Simulation Algorithm**
To estimate the actual significance level ($\hat{\alpha}$), we perform the following steps:

1.  Initialize a counter `rejections = 0`.
2.  **For** $i$ from 1 to 10,000:
    *   Generate a random sample $X_1, X_2, ..., X_{100}$ from a normal distribution $N(1, 4)$.
    *   Calculate the sample variance $S^2 = \frac{1}{99} \sum_{j=1}^{100} (X_j - \bar{X})^2$.
    *   Calculate the test statistic $T_i = \frac{99 \cdot S^2}{4}$.
    *   **If** $T_i > 123.225$, increment `rejections` by 1.
3.  Calculate the estimated $\alpha$: $\hat{\alpha} = \frac{rejections}{10000}$.

**3. Expected Result and Comment**
Since the data is generated exactly under the null hypothesis ($\sigma^2 = 4$), the empirical $\hat{\alpha}$ should be very close to the nominal significance level of $0.05$. Due to Monte Carlo sampling variability, you might get a value like 0.048 or 0.052 (standard error is $\sqrt{0.05 \cdot 0.95 / 10000} \approx 0.002$). This confirms that the test controls the Type I error rate correctly.

---

### **Part (b): Monte Carlo Confidence Interval for $\sigma^2$**

**1. Theoretical Background**
A $100(1-\alpha)\%$ confidence interval for the population variance $\sigma^2$ (assuming normality) is given by:
$$ \left[ \frac{(n-1)S^2}{\chi^2_{1-\alpha/2, n-1}}, \frac{(n-1)S^2}{\chi^2_{\alpha/2, n-1}} \right] $$
For a 95% CI ($\alpha = 0.05$) with $n=100$ ($df=99$):
*   $\chi^2_{0.975, 99} \approx 73.361$
*   $\chi^2_{0.025, 99} \approx 128.422$

**2. Monte Carlo Simulation Algorithm**
To "obtain a confidence interval using the Monte Carlo method", we simulate a sample from the true distribution and construct the CI based on that sample. (Alternatively, in a more advanced simulation, we could generate 10,000 CIs and check their coverage probability).

Here is the process for a single simulated sample:
1.  Generate one random sample of size $n=100$ from $N(1, 4)$.
2.  Calculate the sample variance $S^2$.
3.  Compute the 95% CI using the formula above.

**3. Example Calculation**
Suppose in one Monte Carlo run, the generated sample yields a sample variance of $S^2 = 3.85$.
Plugging this into the formula:
*   Lower Bound: $\frac{99 \cdot 3.85}{128.422} \approx 2.97$
*   Upper Bound: $\frac{99 \cdot 3.85}{73.361} \approx 5.20$
The 95% CI would be $[2.97, 5.20]$.

**4. Advanced Monte Carlo Check (Coverage Probability)**
If the task intends for you to use Monte Carlo to *verify* the CI method, you would:
1.  Generate 10,000 samples of size 100 from $N(1, 4)$.
2.  Calculate the 95% CI for each sample.
3.  Count how many of these 10,000 intervals contain the true variance $\sigma^2 = 4$.
4.  Divide this count by 10,000.

**Comment on Results:**
*   The simulated confidence interval should contain the true population variance ($\sigma^2=4$) approximately 95% of the time.
*   If you run the coverage simulation, you will find the coverage probability is very close to 0.95, validating the theoretical chi-square method for constructing variance confidence intervals.
*   Note that the chi-square confidence interval for variance is asymmetrical (not centered exactly around $S^2$) because the chi-square distribution is skewed, especially for smaller sample sizes. For $n=100$, the skewness is reduced, but still present.

**R Code Snippet for Reproducibility:**
```R
set.seed(123)
n <- 100
mu <- 1
sigma_sq <- 4
sigma <- sqrt(sigma_sq)
reps <- 10000
alpha <- 0.05

# Part (a)
critical_value <- qchisq(1 - alpha, df = n - 1)
rejections <- 0
for(i in 1:reps) {
  x <- rnorm(n, mean = mu, sd = sigma)
  s2 <- var(x)
  T_stat <- (n - 1) * s2 / sigma_sq
  if(T_stat > critical_value) rejections <- rejections + 1
}
estimated_alpha <- rejections / reps
print(paste("Estimated alpha:", estimated_alpha))

# Part (b)
# Generate one sample and calculate CI
x_sample <- rnorm(n, mean = mu, sd = sigma)
s2_sample <- var(x_sample)
lower_chi <- qchisq(alpha/2, df = n - 1)
upper_chi <- qchisq(1 - alpha/2, df = n - 1)
ci <- c((n - 1) * s2_sample / upper_chi, (n - 1) * s2_sample / lower_chi)
print(paste("95% CI for sigma^2: [", round(ci[1], 2), ",", round(ci[2], 2), "]"))
```


Reference:
* https://chat.deepseek.com/a/chat/s/f20fd97e-9855-41d1-a3eb-2f732dfb7dfb