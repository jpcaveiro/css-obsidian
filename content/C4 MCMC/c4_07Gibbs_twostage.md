
# Two stage Gibbs method

DRAFT 

![[Pasted image 20260724143353.png]]

Notice:
* it is necessary to calculate marginal distributions $f_{Y|X}$ and $f_{X|Y}$
* usually $Y_t$ is random observable data given a a certain parameter $X_t$
* and $X_t$ is in parameter space with certain distribution "parametrized" by data [[to do]] improve this.

![[Pasted image 20260724143812.png]]

[[Memory is Something We Do]]

Exercise 1. Simulate:
![[Pasted image 20260724143910.png]]

> [!example]- solution
> mathematica image of f
> ![[Pasted image 20260724143939.png]]
> Plot of the Gibbs trajectory and scatter plot of pXt, Ytq for the bivariate normal (100 iterations)
> ![[Pasted image 20260724143959.png]]
> ![[Pasted image 20260724144017.png]]
> ![[Pasted image 20260724144034.png]]

Exercise 2. Hierarchical Models in Bayesian Analysis. Beta-Binomial model.

![[Pasted image 20260724144148.png]]
![[Pasted image 20260724144245.png]]

> [!example]- solution
> R code
> ![[Pasted image 20260724144312.png]]
> ![[Pasted image 20260724144334.png]]


Exercise 3. Normal hierarquical model (application)

![[Pasted image 20260724144423.png]]

![[Pasted image 20260724144529.png]]

> [!example]- solution
> ![[Pasted image 20260724144558.png]]
> ![[Pasted image 20260724144609.png]]
> ![[Pasted image 20260724144621.png]]
>  

