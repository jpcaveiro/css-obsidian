For data that look like they come from a **mixture of several underlying models**, statisticians usually use **mixture modelling algorithms**. The classic example is a **Gaussian mixture model**, but the same idea applies to mixtures of regressions, mixtures of Poisson models, mixtures of categorical models, etc.

A generic mixture model is:
$$
p(x)=\sum_{k=1}^{K}\pi_k f_k(x \mid \theta_k)
$$
where:
- $x$ is an observed data point,
- $K$ is the number of mixture components,
- $\pi_k$ is the mixing weight for component $k$,
- $f_k(x \mid \theta_k)$ is the model/distribution for component $k$,
- $\theta_k$ are the parameters of component $k$.

The main algorithms used are these.

## Expectation-Maximisation

The most common algorithm is **Expectation-Maximisation**, or **EM**.

It is used when each observation belongs to some hidden component, but you do not know which one.

Example: your data may be a mixture of three Gaussian distributions, but the labels are unknown.

EM alternates between two steps:

### E-step

Estimate the probability that each data point belongs to each component.

For observation $x_i$ and component $k$:
$$
\gamma_{ik}
=
\frac{\pi_k f_k(x_i \mid \theta_k)}
{\sum_{j=1}^{K}\pi_j f_j(x_i \mid \theta_j)}
$$
Here, $$\gamma_{ik}$$ is the posterior probability that point $i$ belongs to component  $k$.
### M-step

Update the model parameters using those probabilities as weights.

For a Gaussian mixture, the updates are roughly:
$$
\pi_k
=
\frac{1}{n}\sum_{i=1}^{n}\gamma_{ik}
$$
$$
\mu_k
=
\frac{\sum_{i=1}^{n}\gamma_{ik}x_i}
{\sum_{i=1}^{n}\gamma_{ik}}
$$
$$
\sigma_k^2
=
\frac{\sum_{i=1}^{n}\gamma_{ik}(x_i-\mu_k)^2}
{\sum_{i=1}^{n}\gamma_{ik}}
$$

EM is widely used because it is simple, efficient, and works well for many mixture models.

## Gaussian mixture models

If the components are Gaussian, the model is called a **Gaussian mixture model**, or **GMM**.

For one-dimensional data:
$$
p(x)=\sum_{k=1}^{K}\pi_k N(x \mid \mu_k,\sigma_k^2)
$$
For multivariate data:
$$
p(x)=\sum_{k=1}^{K}\pi_k N(x \mid \mu_k,\Sigma_k)
$$
GMMs are useful for:

- clustering,
- density estimation,
- anomaly detection,
- modelling heterogeneous populations.

They are usually fitted using EM.

## Mixtures of regressions

Sometimes the mixture is not just of distributions, but of different regression models.

For example, suppose different subgroups follow different linear relationships:

$$
y_i = \beta_{0k}+\beta_{1k}x_i+\epsilon_i
$$

but you do not know which group each observation belongs to.

The mixture model becomes:

$$
p(y_i \mid x_i)
=
\sum_{k=1}^{K}\pi_k
N(y_i \mid \beta_{0k}+\beta_{1k}x_i,\sigma_k^2)
$$

This is called a **mixture of regressions** or **latent class regression**.

It is useful when the data contain multiple hidden behavioural patterns.

Example:

- one customer group is price-sensitive,
- another is brand-loyal,
- another buys randomly.

A single regression would blur these patterns, while a mixture of regressions can separate them.

## Bayesian mixture models

A Bayesian approach puts prior distributions on the parameters.

For example:

$$
\pi \sim \text{Dirichlet}(\alpha)
$$

$$
\theta_k \sim p(\theta_k)
$$

Then we infer the posterior distribution:

$$
p(\pi,\theta,z \mid x)
$$

where $z$ represents the hidden component labels.

Bayesian mixture models are useful when you want:

- uncertainty estimates,
- prior information,
- more robust inference,
- automatic handling of uncertainty about group membership.

Common algorithms include:

- Markov chain Monte Carlo,
- Gibbs sampling,
- Hamiltonian Monte Carlo,
- variational inference.

## Gibbs sampling

**Gibbs sampling** is a Markov chain Monte Carlo method often used for Bayesian mixture models.

It repeatedly samples:

1. the hidden component labels,
2. the component parameters,
3. the mixture weights.

For example:

$$
z_i \sim p(z_i \mid x_i,\pi,\theta)
$$

$$
\theta_k \sim p(\theta_k \mid x,z)
$$

$$
\pi \sim p(\pi \mid z)
$$

It is more computationally expensive than EM, but gives a richer picture of uncertainty.

## Variational inference

**Variational inference** approximates a complicated posterior distribution with a simpler one.

Instead of computing:

$$
p(\pi,\theta,z \mid x)
$$

exactly, we approximate it with:

$$
q(\pi,\theta,z)
$$

and choose $q$ to be close to the true posterior.

Variational inference is often faster than MCMC, especially for large datasets.

It is used in:

- Bayesian Gaussian mixture models,
- topic models,
- latent Dirichlet allocation,
- large-scale clustering.

## Dirichlet process mixtures

If you do not know how many components there should be, you can use a **Dirichlet process mixture model**.

Instead of fixing $K$, the model allows the number of components to grow with the data.

Informally:

$$
K \text{ is inferred from the data}
$$

This is useful when you suspect hidden groups exist but do not know how many.

Common algorithms include:

- Gibbs sampling,
- variational inference,
- Chinese restaurant process samplers,
- stick-breaking approximations.

## K-means as a rough mixture method

**K-means** is not fully probabilistic, but it is closely related to a restricted Gaussian mixture model.

It can be viewed as a simplified case where:

- all clusters are spherical,
- all clusters have equal variance,
- assignments are hard rather than probabilistic.

K-means minimises:

$$
\sum_{i=1}^{n} \sum_{k=1}^{K} r_{ik} \|x_i-\mu_k\|^2
$$

where $$r_{ik}$$ is 1 if point $$i$$ is assigned to cluster $$k$$, and 0 otherwise.

K-means is often used to initialise EM for Gaussian mixture models.

## Hidden Markov models

If the mixture changes over time or sequence position, you may use a **hidden Markov model**, or **HMM**.

An HMM assumes there is a hidden state $$z_t$$ at each time $$t$$, and observations depend on that state:

$$
p(x_t \mid z_t)
$$

The hidden states evolve according to transition probabilities:

$$
p(z_t \mid z_{t-1})
$$

HMMs are used for:

- speech recognition,
- financial regimes,
- biological sequences,
- activity recognition,
- time-series segmentation.

The usual algorithms are:

| Task | Algorithm |
|---|---|
| Estimate hidden states | Forward-backward algorithm |
| Find most likely state sequence | Viterbi algorithm |
| Estimate parameters | Baum-Welch algorithm, an EM variant |

## Model selection methods

A key issue is choosing the number of mixture components $$K$$.

Common methods include:

### AIC

$$
\text{AIC}=2p-2\log L
$$

### BIC

$$
\text{BIC}=p\log n-2\log L
$$

where:

- $$p$$ is the number of estimated parameters,
- $$n$$ is the number of observations,
- $$L$$ is the maximised likelihood.

BIC is especially common for mixture models because it penalises complexity more strongly than AIC.

Other methods include:

- cross-validation,
- held-out likelihood,
- integrated completed likelihood,
- Bayesian nonparametrics,
- posterior predictive checks.

## Common choices by data type

| Data type | Common mixture model |
|---|---|
| Continuous numeric data | Gaussian mixture model |
| Count data | Poisson or negative binomial mixture |
| Binary data | Bernoulli mixture |
| Categorical data | Multinomial mixture |
| Text data | Topic model, latent Dirichlet allocation |
| Time-series data | Hidden Markov model, regime-switching model |
| Regression data | Mixture of regressions |
| Survival data | Mixture cure model or latent class survival model |

## Practical workflow

A typical workflow is:

1. Choose a component family, such as Gaussian, Poisson, or regression.
2. Choose candidate values of $$K$$.
3. Fit each model using EM, Bayesian inference, or variational inference.
4. Compare models using BIC, AIC, cross-validation, or predictive likelihood.
5. Inspect component assignments and parameter estimates.
6. Check whether the inferred components make scientific or practical sense.

## Main algorithms summary

| Algorithm | Main use |
|---|---|
| EM | Standard fitting of finite mixture models |
| Gaussian mixture model | Clustering and density estimation |
| Mixture of regressions | Multiple hidden regression relationships |
| Gibbs sampling | Bayesian mixture inference |
| Variational inference | Fast approximate Bayesian inference |
| Dirichlet process mixture | Unknown number of components |
| K-means | Simple clustering, often used for initialisation |
| Baum-Welch | Hidden Markov models |
| Viterbi | Most likely sequence of hidden states |
| BIC/AIC | Choosing number of components |

The most important one to know first is **EM**. It is the standard workhorse for fitting finite mixture models when the group labels are hidden.
