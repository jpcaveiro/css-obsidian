
There are several ways to measure the difference between two probabilities, each suited to a different question. Here are the most common ones.

## 1. Absolute difference (risk difference)

$$
\Delta = p_1 - p_2
$$

The simplest measure. It tells you the difference in absolute terms and is directly interpretable as a change in probability.

- Range: $[-1, 1]$
- Often used in epidemiology and clinical trials as the **absolute risk reduction**.
- Symmetric and bounded, but its variance depends on the magnitude of $p_1, p_2$.

## 2. Relative risk (risk ratio)

$$
RR = \frac{p_1}{p_2}
$$
Tells you how many times more likely one event is than the other.

- Range: $[0, \infty)$, with 1 meaning "no difference"
- Asymmetric: $RR = 2$ and $RR = 0.5$ are inverse in magnitude but not in number. Taking $\log(RR)$ fixes this, giving a symmetric measure on $(-\infty, \infty)$ centered at 0.

## 3. Odds ratio

$$
OR = \frac{p_1/(1-p_1)}{p_2/(1-p_2)}
$$

Compares the **odds** rather than the probabilities.

- Range: \([0, \infty)\), 1 = no difference
- Very common in logistic regression and case-control studies.
- The **log odds ratio** \(\log(OR)\) is symmetric around 0 and is approximately normally distributed, which makes it convenient for confidence intervals and hypothesis testing.

## 4. Distance/divergence measures

When you want a **metric** between probability distributions (especially for simulation, information theory, or model comparison):

- **KL divergence**: \(D_{KL}(p \| q) = \sum p_i \log(p_i/q_i)\). Not symmetric and not a true distance.
- **Jensen-Shannon divergence**: a symmetrized, smoothed version of KL. It's symmetric, always finite, and its square root is a true metric (Jensen-Shannon distance).
- **Total variation distance**: \(\frac{1}{2}\sum |p_i - q_i|\). Simple, symmetric, bounded in \([0,1]\).
- **Hellinger distance** and **Bhattacharyya distance**: useful when comparing distributions and caring about smooth behavior near zero probabilities.

## 5. For testing, not just describing

If the goal is inference, the difference is usually quantified with a **confidence interval** or a **hypothesis test** built on one of the above:

- Two-proportion **z-test** on \(p_1 - p_2\)
- **Fisher's exact test** or **chi-square test** on the underlying contingency table
- Confidence interval for the log odds ratio or log relative risk (often preferred because the sampling distribution is better approximated as normal on the log scale).

## Choosing between them

| Question you're asking | Use |
|---|---|
| What's the absolute change in probability? | Risk difference \(p_1 - p_2\) |
| How many times more likely? | Relative risk |
| How do odds compare (logistic model)? | Odds ratio |
| How different are two full distributions? | JS distance, total variation |
| Is the difference statistically significant? | z-test / Fisher / chi-square |

A practical rule: for **communication** (reports, clinical contexts) use risk difference and relative risk; for **modeling and inference** use the log odds ratio; for **comparing distributions** in simulation/information-theoretic work use Jensen-Shannon or total variation distance.

If you tell me the specific setting you're working in (e.g., comparing two estimators, evaluating a classifier, a clinical trial, or a simulation in R), I can recommend the right measure and show you the code.

Reference:
* https://www.perplexity.ai/computer/tasks/f97280b8-b9b2-49a1-8204-f91f9d6fb8f2