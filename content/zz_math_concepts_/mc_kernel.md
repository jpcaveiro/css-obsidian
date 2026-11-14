# Kernel

Now the notation used in this documentation.

[[definition]] "Transition Kernel" and "Kernel Probability"
![[Pasted image 20260722094132.png]]

About notation with "$K$" symbol:
* "kernel" word describes a central step: kernel is used to propose moves $X_t \mapsto X_{t+1}$
* When $K$ is used in "$\cdots \sim K$ " then $K$ is seen as a distribution.
* When $K$ is used like 

	$$\int_{\chi} K(y|x) f(x) dx = f(y)$$
	 
	* then $K$ is seen as probability density;
	* the state space of integral is represented by chi letter ($\chi\subset \mathbb{R}^n$) which is the set of all possible regions or values the sequence can visit.

[[Further reading]]:  [[LLM C4 more on Markov kernel]].
