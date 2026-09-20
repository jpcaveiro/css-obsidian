In statistics, “mixtures of variables” usually refers to **mixture models**: models where the observed data are assumed to come from a combination of several underlying groups or distributions.

A typical mixture model looks like:
$$
p(x)=\sum_{k=1}^{K}\pi_k f_k(x)
$$
where:
- $x$ is the observed variable,
- $K$ is the number of hidden groups or components,
- $f_k(x)$ is the distribution of component $k$,
- $\pi_k$ is the weight or probability of belonging to component $k$,
- and the weights satisfy:
$$
\sum_{k=1}^{K}\pi_k=1
$$
They are useful for several things.
## Finding hidden groups

Mixture models are often used for **clustering** when the groups are not directly observed.

Example: suppose you have height data from a population containing children and adults. The overall distribution may look like a mix of two different distributions: one for children, one for adults.

So instead of assuming one single normal distribution, you might model the data as:

$$
p(x)=\pi_1 N(\mu_1,\sigma_1^2)+\pi_2 N(\mu_2,\sigma_2^2)
$$

This means the data are treated as coming from two normal distributions mixed together.

## Modelling complex distributions

Real-world data are often not nicely bell-shaped. Mixtures can model:

- skewed distributions,
- distributions with several peaks,
- heavy-tailed data,
- unusual subpopulations.

For example, income data may contain several groups: students, full-time workers, retirees, executives, etc. A single distribution may fit badly, but a mixture can capture the structure better.

## Probabilistic classification

Mixture models can assign each observation a probability of belonging to each group.

For example, a customer might be classified as:

| Segment | Probability |
|---|---:|
| Budget buyer | 0.70 |
| Occasional buyer | 0.20 |
| Premium buyer | 0.10 |

This is useful because it avoids forcing a hard classification when there is uncertainty.

## Detecting outliers

Mixtures can separate “ordinary” observations from unusual ones.

For example, in fraud detection, most transactions may come from a normal-spending component, while suspicious transactions may belong to a rare component with different behaviour.

## Handling population heterogeneity

A mixture model is useful when the population is not homogeneous.

Examples:

- patients with different disease subtypes,
- customers with different buying patterns,
- students with different learning profiles,
- genes with different expression patterns,
- financial returns under calm versus crisis regimes.

## Useful in machine learning

Mixture models are common in:

- Gaussian mixture models,
- topic modelling,
- hidden Markov models,
- Bayesian clustering,
- density estimation,
- anomaly detection.

For example, a **Gaussian mixture model** assumes that the data come from several Gaussian components rather than one.

## If you mean mixed types of variables

Sometimes people use “mixtures of variables” to mean datasets containing different variable types, such as:

- numerical variables,
- categorical variables,
- ordinal variables,
- binary variables.

That is useful because many real datasets contain mixed information.

Example:

| Variable | Type |
|---|---|
| Age | numerical |
| Gender | categorical |
| Education level | ordinal |
| Has diabetes | binary |
| Income | numerical |

Methods for mixed variables are useful in surveys, medicine, economics, psychology, and social sciences.

In that sense, “mixtures of variables” are useful because they let you analyse richer datasets that cannot be described by numerical variables alone.