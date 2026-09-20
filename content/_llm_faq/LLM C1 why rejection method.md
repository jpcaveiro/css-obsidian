

## Random generation based on rejection method

Rejection (acceptance–rejection) sampling generates random variates from a target distribution by proposing candidates from an easy-to-sample proposal distribution and accepting each candidate with probability proportional to the ratio of target to scaled proposal; it is simple to implement and works for continuous and discrete targets when the inverse CDF is impractical.

How the method works

- Choose a proposal density q(x) you can sample from and a constant M ≥ sup_x p(x)/q(x) so that M q(x) ≥ p(x) for all x.
    
- Repeat: draw Y ~ q, draw U ~ Uniform(0,1). Accept Y as a sample from p if U ≤ p(Y) / (M q(Y)); otherwise reject and repeat.
    
- The accepted values follow the target distribution p(x), and the number of trials until acceptance is geometric with mean M (so expected acceptance probability is 1/M).
    

Practical choices and efficiency

- Good q reduces M and increases acceptance rate; choose q that matches p’s shape (same tails and mode locations).
    
- If p has heavier tails than common q choices, acceptance can be very low; use a fatter-tailed q (e.g., Student-t for fat-tailed p).
    
- For multi-modal p, use a mixture proposal that places mass near each mode.
    
- For discrete targets, pick q as an easy discrete distribution and the same acceptance test applies using pmfs.
    

Implementation notes (pseudo-code)

- Precompute or bound M; if p(x) is known only up to a constant factor, you can often work with unnormalized p by using the same constant in numerator and denominator if q is normalized.
    
- Use log densities for numerical stability: accept if log U ≤ log p(Y) − log q(Y) − log M.
    
- If M unknown, you can search for a minimal M numerically or use adaptive schemes (careful—must preserve correctness).
    

When to prefer rejection sampling

- Use when inverse-CDF is hard and you can find an easy proposal q with reasonably small M.
    
- Good for low-to-moderate dimensions; in high dimensions acceptance usually collapses (so prefer MCMC or importance sampling variants).
    

Variants and improvements

- Adaptive rejection sampling (ARS) for log-concave densities builds a piecewise-envelope q that tightly bounds p, achieving high efficiency.
    
- Ratio-of-uniforms, transformed rejection, and slice sampling are related methods often more efficient for certain families.
    
- For multi-dimensional problems, consider importance sampling, Metropolis–Hastings, or other MCMC when rejection becomes impractical.
    

Simple example (conceptual)

- To sample from p(x) on [a,b] where p is bounded: take q uniform on [a,b] and M = max_x p(x)·(b−a). Propose Y ~ Uniform[a,b], U ~ Uniform(0,1); accept if U ≤ p(Y)/p_max. Accepted Y follow p.
    

Would you like a short verified Python example using numpy (with log-density handling and a small demonstration), or help choosing a proposal q and M for a specific target distribution you have?

## Examples where inverse CDF is impractical

Examples where the inverse CDF is impractical include the **normal distribution**, because its CDF has no simple closed-form inverse, and many **truncated or custom distributions**, where the CDF inverse must be computed numerically and can be slow or inaccurate.[[eg.bucknell](https://www.eg.bucknell.edu/~xmeng/Course/CS6337/Note/master/node55.html)]

Common cases are:

- **Normal and related bell-shaped laws**: no closed-form quantile function, so inverse sampling usually relies on numerical approximations.[[github](https://github.com/benroberts999/InverseNumericalCDF)]
    
- **Truncated normal distributions**: the inverse is only available through the underlying normal quantile function and can become expensive when truncation is extreme.[[youtube](https://www.youtube.com/watch?v=TR0biDues7k)]
    
- **Custom distributions defined only numerically or by simulation**: if the CDF itself is expensive to evaluate, inverting it repeatedly is often impractical.[[discourse.julialang](https://discourse.julialang.org/t/approximating-the-inverse-of-an-expensive-cdf-function/114809)]
    
- **Distributions with awkward tails or piecewise definitions**: even when an inverse exists in theory, it may be hard to compute robustly and efficiently in practice.[[en.wikipedia](https://en.wikipedia.org/wiki/Inverse_transform_sampling)]
    

In those cases, rejection sampling is attractive because it avoids solving F−1(u)F^{-1}(u)F−1(u) directly and instead uses a proposal distribution plus an accept/reject test.[[eg.bucknell](https://www.eg.bucknell.edu/~xmeng/Course/CS6337/Note/master/node55.html)]