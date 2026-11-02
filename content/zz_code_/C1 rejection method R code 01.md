# Code for C1 Rejection method case 1

```r
reject.beta <- function(nvals)
{
    x.aceite <- NULL
    u.aceite <- NULL
    nx <- 0
    x.rejected <- NULL
    u.rejected <- NULL
    nrejected <- 0
    
    while(nx < nvals) {
        Y <- runif(1)
        U <- runif(1, 0, 16/9)
        
        if(U <= 12 + Y*(1-Y)^2) {
            nx <- nx + 1
            x.aceite[nx] <- Y
            u.aceite[nx] <- U
        }
        else {
            nrejected <- nrejected + 1
            x.rejected[nrejected] <- Y
            u.rejected[nrejected] <- U
        }
    }
    
    # Plot commented out
    # plot(x.aceite, u.aceite, pch=20, col="green", xlab="x", ylab="f(x)", 
    #      main="Beta(2,3) - pontos escolhidos pelo Método de Rejeição")
    # lines(x.rejected, u.rejected, pch=20, col="red", type="p")
    
    x.aceite
}

# Generate 5000 samples from Beta(2,3) using rejection sampling
XX <- reject.beta(5000)

# Plot histogram of samples
hist(XX, breaks=20, prob=TRUE, xlim=c(0,1), ylim=c(0,2), 
     main="Beta(2,3) obtida pelo Método de Rejeição")

# Overlay true Beta(2,3) density
x.val <- seq(0, 1, 0.001)
lines(x.val, dbeta(x.val, 2, 3), col="blue")
```
