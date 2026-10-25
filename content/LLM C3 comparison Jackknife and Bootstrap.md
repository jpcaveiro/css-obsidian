## Bootstrap vs. Jackknife

This comparison covers the ordinary nonparametric bootstrap and the delete-one jackknife for i.i.d. observations; dependent or clustered data require adapted resampling schemes.

### How each method works

The **jackknife**, introduced by Quenouille (1949) and developed by Tukey (1958), systematically deletes each observation in turn: from a sample of size $n$ you get exactly $n$ subsamples of size $n-1$, recalculating the statistic on each. The **bootstrap** (Efron, 1979) instead draws $B$ random samples of size $n$ from the data with replacement, treating the sample itself as an estimate of the population. Efron's original paper was pointedly titled "Bootstrap methods: another look at the jackknife". [onlinelibrary.wiley](https://onlinelibrary.wiley.com/doi/full/10.1111/1755-0998.70148)

The core estimates are:

$$
\widehat{\operatorname{bias}}_J = (n-1)(\hat\theta_{(\cdot)} - \hat\theta), \qquad
\widehat{\operatorname{se}}_J = \sqrt{\frac{n-1}{n}\sum_{i=1}^n \left(\hat\theta_{(i)} - \hat\theta_{(\cdot)}\right)^2}
$$

for the jackknife, where $\hat\theta_{(i)}$ is the statistic computed without observation $i$, while the bootstrap standard error is simply the standard deviation of the $B$ replicate statistics. [bioconductor](https://www.bioconductor.org/help/course-materials/2003/NGFN03/resampling.pdf)

### Comparison table

| Aspect | Jackknife | Bootstrap |
|---|---|---|
| Resampling mechanism | Systematic leave-one-out: $n$ subsamples of size $n-1$ [onlinelibrary.wiley](https://onlinelibrary.wiley.com/doi/full/10.1111/1755-0998.70148) | Random resampling with replacement: $B$ samples of size $n$ [medcalc](https://www.medcalc.org/en/book/bootstrap-jackknife.php) |
| Number of statistic evaluations | Exactly $n$, fixed by sample size ([arXiv:1907.12851](http://www.arxiv.org/pdf/1907.12851v1)) | $B$, chosen by the analyst (typically 1000+) ([arXiv:1907.12851](http://www.arxiv.org/pdf/1907.12851v1)) |
| Determinism | Deterministic — same result every run [jaqm](https://www.jaqm.ro/issues/volume-2,issue-2/pdfs/sahinler_topuz.pdf) | Stochastic — adds Monte Carlo error, though reproducible with a fixed seed [jaqm](https://www.jaqm.ro/issues/volume-2,issue-2/pdfs/sahinler_topuz.pdf) |
| What it estimates | Primarily bias and standard error [bioconductor](https://www.bioconductor.org/help/course-materials/2003/NGFN03/resampling.pdf) | Approximates the whole sampling distribution — spread, shape, skewness — enabling percentile confidence intervals [medcalc](https://www.medcalc.org/en/book/bootstrap-jackknife.php) |
| Statistical type required | Smooth (differentiable) statistics only [bioconductor](https://www.bioconductor.org/help/course-materials/2003/NGFN03/resampling.pdf) | No smoothness restriction — its main advantage as a general-purpose tool [medcalc](https://www.medcalc.org/en/book/bootstrap-jackknife.php) |
| Relation to bootstrap | A linear (first-order) approximation to the bootstrap [link.springer](http://link.springer.com/content/pdf/10.1007%2F978-1-4612-4380-9_41.pdf) | The more general method; jackknife ≈ "$[n/(n-1)]^{1/2}$ times a bootstrap" for the linearized statistic [sites.stat.washington](https://sites.stat.washington.edu/courses/stat527/s13/readings/EfronGong_am_stat1983.pdf) |

### The relationship in detail

The jackknife is best understood as a linearization of the bootstrap: Efron showed it approximates the bootstrap by fitting a linear function to the statistic on the simplex of resampling weights, so for linear statistics the two nearly agree — for the sample mean, $\widehat{\operatorname{Var}}_J(\bar X) = s^2/n$ versus the ideal bootstrap variance $\frac{n-1}{n}\frac{s^2}{n}$ — and for quadratic statistics they differ only by a normalizing factor (Efron 1979; [arXiv:1907.12851](http://www.arxiv.org/pdf/1907.12851v1)). Because jackknife subsamples overlap so heavily with the original data, the raw spread of leave-one-out replicates understates the true standard error and should not be used like a bootstrap standard deviation; the correction formula above is required (Wiley; UC Berkeley notes). [stat.berkeley](https://www.stat.berkeley.edu/~hhuang/STAT152/Jackknife-Bootstrap.pdf)

### Where the jackknife fails

The delete-one jackknife requires the statistic to change smoothly when one observation is removed; it can give inconsistent variance estimates for sample quantiles such as the median, where leave-one-out estimates collapse to a handful of distinct values whose spread bears no reliable relation to the true standard error (MedCalc; TCD lecture notes). The bootstrap is consistent for regular quantiles under conditions such as i.i.d. sampling and a continuous, positive density at the target quantile — no smoothness of the statistic itself is needed. The delete-$d$ jackknife (removing groups of $d$ observations) can extend the jackknife to such statistics when $d$ is suitably chosen. [csyue.nccu.edu](http://csyue.nccu.edu.tw/ch/Jackknife_Notes.pdf)

### When to use which

The bootstrap is the more general approach for approximating sampling distributions and constructing confidence intervals when its validity conditions hold, at the cost of $B$ evaluations and Monte Carlo error (MedCalc; JAQM). The jackknife offers deterministic bias and standard-error estimates for sufficiently regular statistics using exactly $n$ leave-one-out fits — so which is cheaper depends on whether $n$ is smaller or larger than your chosen $B$, and the jackknife remains attractive for bias reduction of smooth estimators and in complex sampling designs where it is easier to apply ([Efron & Tibshirani via arXiv:1907.12851](http://www.arxiv.org/pdf/1907.12851v1); JAQM). [jaqm](https://www.jaqm.ro/issues/volume-2,issue-2/pdfs/sahinler_topuz.pdf)