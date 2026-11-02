
See [[LLM C4 what is a kernel]].

Now the notation used in this documentation.

[[definition]] "Transition Kernel" and "Kernel Probability"
![[Pasted image 20260722094132.png]]

About notation "$K$":
* "kernel" is used because its what allows moves under a distribution.
* When $K$ is used in "$\cdots \sim K$ " then $K$ is seen as a distribution.
* When $K$ is used like 
	* $\int_{\chi} K(y|x) f(x) dx = f(y)$ 
	* then $K$ is seen as a probability
	* where $\chi$ is the state space ($\subset \mathbb{R}^n$) which is the set of all possible regions or values the sequence can visit

