# Markov Chain

A Markov Chain has a fundamental property that the probability of changing to another state depends only on current state and then new state is drawn from a Kernel distribution.

![[mc_markovchain]]

![[mc_kernel]]


[[example]]
![[Pasted image 20260722094935.png]]

From Example 1.1 one can write:

$$K(X_{t+1}|(\text{given }X_t=x_t)) = N(x_t, 1)$$

so the distribution of $X_{t+1}$ is $N(x_t, 1)$ and $X_{t+1}$ will be drawn from $K(X_{t+1}|X_t=x_t)$  i.e., in this example is from distribution $N(x_t,1)$.

[[Further reading]] (and visualizing):

* Introductory video by Kapil Sachdeva: [Markov Chains - VISUALLY EXPLAINED + History!](https://youtu.be/CIe869Rce2k?si=Rl_3z3g2VM7wJJ0c)  
* An important property to be verified is the [[mc_stationary|stationary probability distribution in Markov Chains]].
