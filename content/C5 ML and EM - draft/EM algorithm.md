
![[Pasted image 20260724130155.png]]

Notes:
* bold $y$ and $z$ symbols mean they are vectors.
* $L(\theta|y,z)$ mean "theta given (y and z)"
* $f(y,z|\theta)$ mean (y and z) given theta. $f$ is the same expression as $L$.
* [[to do]] check all of this

## Motivation

![[Pasted image 20260724130447.png]]
[[to do]] find more motivations

# Making EM algorithm

![[Pasted image 20260724130523.png]]

Notes:
* since $z$ is hidden from observation (called a latent vector variable) then
	* $f(y|\theta)$ is a marginal density of full $f( (y,z)\text{ given } \theta)$.
	* or, using $L$ notation
	* $$
	\int L(\theta \text{ given } (y,z)) dz$$
	* $\log$...

![[Pasted image 20260724130951.png]]
[[to do]] explain deductions


# EM algorithm

![[Pasted image 20260724131055.png]]

# Considerations

![[Pasted image 20260724131232.png]]

# References

![[Pasted image 20260724131248.png]]

[[to do]] E codificar em R?

