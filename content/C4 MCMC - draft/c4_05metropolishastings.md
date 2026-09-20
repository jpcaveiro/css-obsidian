# Need for asymmetrical proposal distribution

Drawing from the sources and our conversation history, here are three examples of **asymmetrical proposal distributions ($q$)** used in the Metropolis-Hastings (M-H) algorithm:

1. **State-Dependent Chi-Square Distribution:** In some simulations, such as generating values for a **Rayleigh distribution**, the candidate value $y$ is suggested using a **chi-square distribution** where the degrees of freedom are determined by the current state of the chain: $q(y|x) \sim \chi^2_x$. This is inherently asymmetric because the probability of proposing $y$ from $x$ does not equal the probability of proposing $x$ from $y$ ($q(y|x) \neq q(x|y)$) due to the shape of the chi-square density changing based on its degrees of freedom.
    
2. **Fixed Densities in Independent Metropolis-Hastings:** In the **Independent M-H algorithm**, the candidate value $y$ is generated independently of the current state $x$, meaning the proposal distribution is constant: $q(y|x) = q(y)$. Unless the chosen density $q(y)$ is perfectly symmetric around the same point as the target distribution $f(y)$, the proposal process is asymmetric because the forward transition density ($q(y)$) typically differs from the backward transition density ($q(x)$) . This approach is often used when a known density $q(y)$ is a good approximation of the target density $f(y)$ .
    
3. **Proposals for Multivariate Exploration (Directional "Pushing"):** In complex **multivariate models**, simple symmetric random walks can be quite inefficient . In these cases, asymmetric proposal distributions are designed to **"push" the chain more effectively** toward high-probability regions or along specific correlation structures . By utilizing non-symmetric transition rules that favor movement in certain directions, the algorithm can explore high-dimensional spaces more efficiently than a standard symmetric proposal .

![[Pasted image 20260724002946.png]]

[[Memory is Something We Do]]:
* [[Ex 4-mh-01]]
* 

![[Pasted image 20260724003529.png]]

![[Pasted image 20260724003547.png]]

![[Pasted image 20260724003601.png]]

![[Pasted image 20260724003614.png]]
![[Pasted image 20260724003624.png]]












 

