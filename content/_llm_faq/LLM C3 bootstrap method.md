
The **bootstrap method** is a computer-intensive statistical technique that estimates the sampling distribution of a statistic by repeatedly resampling **with replacement** from your observed data.  [machinelearningmastery](https://machinelearningmastery.com/a-gentle-introduction-to-the-bootstrap-method/) It lets you quantify uncertainty (standard errors, confidence intervals, hypothesis tests) without relying on strong theoretical assumptions like normality.  [youtube](https://www.youtube.com/watch?v=5aLeFVbVoJg)

## Core idea

Instead of deriving complicated formulas for how a statistic (e.g., mean, median, regression coefficient) varies from sample to sample, the bootstrap treats your single observed sample as a stand-in for the population and simulates many “new” samples from it.  [youtube](https://www.youtube.com/watch?v=o9_NmnbRz88)

- You draw a **bootstrap sample**: same size as the original, sampled **with replacement**.  [youtube](https://www.youtube.com/watch?v=o9_NmnbRz88)
- You compute the statistic of interest on that bootstrap sample.  [youtube](https://www.youtube.com/watch?v=5aLeFVbVoJg)
- You repeat this thousands of times (e.g., 1,000–10,000) to build an **empirical bootstrap distribution** of the statistic.  [youtube](https://www.youtube.com/watch?v=o9_NmnbRz88)
- From that distribution you estimate standard error, bias, and confidence intervals.  [youtube](https://www.youtube.com/watch?v=o9_NmnbRz88)

This works because the variability present in your sample approximates the variability in the underlying population, especially as sample size grows.  [youtube](https://www.youtube.com/watch?v=5aLeFVbVoJg)

## Why use it?

- **Few assumptions**: Doesn’t require normality or other strict distributional forms.  [youtube](https://www.youtube.com/watch?v=5aLeFVbVoJg)
- **Complex statistics**: Works for medians, ratios, machine-learning performance metrics, etc., where theory is messy or unavailable.  [machinelearningmastery](https://machinelearningmastery.com/a-gentle-introduction-to-the-bootstrap-method/)
- **Small or awkward samples**: Often more reliable than asymptotic approximations when theory-based methods are dubious.  [youtube](https://www.youtube.com/watch?v=o9_NmnbRz88)
- **Model assessment**: Used in machine learning to estimate prediction error and stability via resampling.  [machinelearningmastery](https://machinelearningmastery.com/a-gentle-introduction-to-the-bootstrap-method/)

## Basic algorithm (step by step)

Given data $$x_1, \dots, x_n$$ and a statistic (e.g., mean) $$T$$
Step 1. Compute $T$ on the original data.

Step 2. For $b = 1, \dots, B$ (e.g., $B = 10\,000$):
   - Draw a bootstrap sample $$x^{*(b)}_1, \dots, x^{*(b)}_n$$ by sampling $n$ times **with replacement** from $(x_1, \dots, x_n)$.  
   - Compute $$T^{*(b)} = T(x^{*(b)}_1, \dots, x^{*(b)}_n)$$
Step 3. Use the collection $$\left(T^{*(1)}, \dots, T^{*(B)}\right)$$ as an approximation to the sampling distribution of $T$.  

From this distribution you can:

- Estimate **standard error**: $$\widehat{SE}(T) = \sqrt{\frac{1}{B-1}\sum_{b=1}^B \left(T^{*(b)} - \overline{T^*}\right)^2}$$
- Build a **95% confidence interval** using percentiles: take the 2.5th and 97.5th percentiles of $(T^{*(b)})$.
- Assess **bias**: $$\widehat{\text{Bias}} = \overline{T^*} - T_{\text{original}}$$
## Simple example

Suppose you have 10 observations and want a confidence interval for the **median**:

- Resample 10 values with replacement from your data → bootstrap sample 1 → compute its median.
- Repeat 10 000 times → 10 000 bootstrap medians.
- The 2.5th and 97.5th percentiles of those 10 000 medians give a 95% bootstrap confidence interval for the population median. 

## Limitations and cautions

- **Very small samples**: Bootstrap can be unstable if $n$ is extremely small.
- **Dependent data**: Standard i.i.d. bootstrap assumes independent observations; for time series or clustered data you need specialized variants (e.g., block bootstrap).  [www3.wabash](http://www3.wabash.edu/econometrics/EconometricsBook/chap23.htm)
- **Not a magic fix**: If the original sample is badly biased or unrepresentative, the bootstrap will reflect that. 

The method was introduced by **Bradley Efron** in 1979 and is now a standard tool in statistics, econometrics, and data science.  

References:
* [youtube](https://www.youtube.com/watch?v=o9_NmnbRz88) (o mais citado neste texto gerado)
* [youtube](https://www.youtube.com/watch?v=5aLeFVbVoJg)
* [sciencedirect](https://www.sciencedirect.com/topics/computer-science/bootstrap-method)