# Motivation

## Use in Simulation

![[Pasted image 20260617142339.png]]

Exercise. $U_1, U_2, \ldots, U_n$ are independent random variables with uniform distribution, $U_{[0;1]}$. Which distribution has
$$
Y = \sum_{i=1}^{12} U_i - 6  \quad ?
$$
1. Check analytical solution of $Y$ [here](https://en.wikipedia.org/wiki/Irwin%E2%80%93Hall_distribution).
2. Considering $Y\sim_{aprox} Normal$ what will be its parameters?
3. What to do if no analytical solution is available?

> [!example]- solutions
> 1. "Irwin–Hall distribution"
> 2. $N(0;1)$
> 3. Maybe simulations! The reason of this course.

## Use as Numerical integration

![[Pasted image 20260617142451.png]]

* Note: next section will be dedicated to this notation and concepts.

Exercise
1. Why $f(u)$ disapears in second line?

> [!example]- solution
> $f(u)=1$ in $0 \le u \le 1$ because its uniform distribution.


---

![[Pasted image 20260617142501.png]]

[[Further Reading]]:  
* [[LLM C2 numeric methods vs Monte Carlo methods|When to use standard numerical approximation rules?]]
* [[motivation|Other motivations]]
