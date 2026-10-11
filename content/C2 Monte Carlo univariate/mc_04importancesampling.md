# MC Importance Sampling

First recalll the context of this section and [[mc_03probabilities|the difficulty of generating rare events]].

![[Pasted image 20260717103228.png]]

A [[heavy tail]] is a distribution whose probabilities decrease slowly for extreme values, so unusually large or small observations are more common than in a normal or exponential distribution. It often leads to many outliers and may make the mean or variance unstable or even infinite.

![[Pasted image 20260717103312.png]]

[[Memory is Something We Do]]: [[explain]] and [[run R code|run the following R code]]:
```r
par(mfrow = c(2, 2))
a <- 4.5

for (i in 2:5) {
  N <- 10^i
  y <- rexp(N) + a    # proposal: exponential shifted by a (support y > a)
  fdivg <- dnorm(y) / dexp(y - a)  # importance weights f(y)/g(y)
  vect <- cumsum(fdivg) / 1:N      # running estimate of P(Z > a)
  plot(vect, type = "l", main = paste("N =", N), ylab = "p.hat")
  abline(h = pnorm(-a), col = "green")  # true value P[Z > 4.5] = P[Z < -4.5]
  cat("N=", N, "p.hat=", vect[N], " p=", pnorm(-a),
      "dif=", abs(vect[N] - pnorm(-a)), "\n")
}
```


> [!example]- a solution
> (Why your solution could be similar but not equal?)
> ![[Pasted image 20261002112745.png]]
> ![[Pasted image 20260717103345.png]]


![[Pasted image 20260717103412.png]]

(There is an exercise above!)

