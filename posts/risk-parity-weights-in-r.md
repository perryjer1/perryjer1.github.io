<!-- 
.. title: Risk Parity Weights in R
.. slug: risk-parity-weights-in-r
.. date: 2017-05-05 13:50:55 UTC-05:00
.. tags: R
.. category: 
.. link: 
.. description: 
.. type: text
-->

Every now and then I need to calculate risk parity weights in R. I
like to know how things are working under the hood and the solutions I
found were a little opaque. Fortunately I found a nice article that
gives a straightforward algorithm,
see [here](http://www.iinews.com/site/pdfs/joi_fall_2012_ra1.pdf).

Here is my R code to implement it. This is from the "Algorithm 1:
Newton's method" section in the paper.

```R
riskparity <- function(sigma, tol = 1e-7, maxeval = 1000) {
  F <- function(x, lambda) {
    mat <- sigma %*% x - lambda * 1/x
    rbind(mat, sum(x) - 1)
  }

  J <- function(x, lambda) {
    mat <- sigma + lambda * diag(1/x^2)
    mat <- rbind(mat, rep(1, ncol(sigma)))
    cbind(mat, c(-1/x, 0))
  }

  w <- 1 / sqrt(diag(sigma))
  w <- c(w / sum(w), 0.5) # add guess for lambda at the end
  N <- length(w)

  cureval <- 0
  while (cureval < maxeval) {
    cureval <- cureval + 1
    wn <- w - solve(J(w[-N], w[N])) %*% F(w[-N], w[N])
    if (sqrt(sum(wn - w)^2) < tol) {
      return(list(w = w[-N], lambda = w[N], status = "converge"))
    }
    w <- wn
  }

  list(w = w[-N], lambda = w[N], status = "maxeval")
}
```
