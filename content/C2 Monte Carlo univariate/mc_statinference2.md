# distribution and quantile approximation

Is what follows recall MC will generate $N$ sets of samples of size $n$:

* $X_1^{(1)}, X_2^{(2)}, \ldots,X_n^{(1)}$ (first sample of size $n$)
* ... and so on ...
* $X_1^{(N)}, X_2^{(N)}, \ldots,X_n^{(N)}$ (last sample of size $n$).

and for each sample a estimation is done with some statistics $T$:
* $T^{(1)} = T(\text{sample 1})$
* and so on
* $T^{(N)} = T(\text{sample N})$

## distribution approximation

Given $x$ what is the probability $P(T \le x)$?
![[Pasted image 20260717113501.png]]


## quantile point and interval estimation

In what follows:
* Here $\chi_{p,T}$ is the quantile of order $p$ from $T$ distribution.
* $N$ is the sample size
* $p$ is an order
* $Np$ is $N \times p$.

Given $p\in[0,1]$ what is the quantile $\chi_{p,T}$ that solves $P(T \le \chi_{p,T}) =p$?
![[Pasted image 20260720101401.png]]



## confidence interval for median and other quantiles

![[Pasted image 20260717113727.png]]


