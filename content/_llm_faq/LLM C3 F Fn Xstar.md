
![[Pasted image 20260720105529.png]]

The image is showing the two main ways to think about the bootstrap in statistics. It contrasts the **true data-generating process** with the **empirical resampling process** used in practice. 

## What the arrows mean

- $F \to X \to F_n$: this is the usual statistical story.
- $F$ is the unknown true population distribution.
- $X$ is the observed sample drawn from $F$.
- $F_n$ is the empirical distribution built from that sample. 

- $F_n \to X^* \to F_n^*$: this is the bootstrap story.
  - Start from the empirical distribution $F_n$, not the unknown $F$.
  - Draw a bootstrap sample $X^*$ from $F_n$, with replacement.
  - Compute the bootstrap empirical distribution $F_n^*$ from that resample.

## Main idea

The bootstrap replaces the unknown population distribution $F$ with the empirical distribution $F_n$ estimated from your data. Then it repeatedly resamples from $F_n$ to mimic what new samples from $F$ might look like. 

## Why this matters

This is how the bootstrap estimates uncertainty, such as standard errors or confidence intervals, without needing a full parametric model for $F$.

A simple way to read the picture is: **real world** $\to$ observed sample $\to$ estimated distribution, then **estimated distribution** $\to$ resampled data $\to$ bootstrap version of the distribution.