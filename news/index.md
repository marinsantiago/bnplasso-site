# Changelog

## bnplasso 0.2.1

- The package now includes the functions
  [`psis.loo()`](../reference/psis.loo.md) and
  [`widely.aic()`](../reference/widely.aic.md), which compute the
  Pareto-smoothed importance sampling leave-one-out information
  criterion (PSIS-LOO) and the Watanabe–Akaike information criterion
  (WAIC), respectively.
- GitHub version: [marinsantiago/bnplasso@6adfa6d]()

## bnplasso 0.2.0

- The functions `blasso.lm()` and `balasso.lm()` have been merged into
  the function, [`bnplasso.lm()`](../reference/bnplasso.lm.md). A new
  argument, `prior`, has been introduced in
  [`bnplasso.lm()`](../reference/bnplasso.lm.md), which specifies the
  type of shrinkage prior that should be employed. The options are: (a)
  a nonparametric Bayesian Lasso prior (default), (b) a Bayesian Lasso
  prior, or (c) a Bayesian adaptive Lasso prior.
- The [`bnplasso.lm()`](../reference/bnplasso.lm.md) function now
  supports single-precision floating-point calculations for certain
  internal routines via the `float` argument. By default, the function
  still uses double point precision.
- By default, the [`bnplasso.lm()`](../reference/bnplasso.lm.md)
  function now includes an intercept term in the regression function.
- The [`bnplasso.lm()`](../reference/bnplasso.lm.md) function now
  returns the log-likelihood of each observation at each MCMC iteration.
- If some user-supplied hyperparameters are not provided, the
  [`bnplasso.lm()`](../reference/bnplasso.lm.md) function will now
  attempt to automatically determine appropriate values for those
  hyperparameters.
- The package now includes the function
  [`get.partition()`](../reference/get.partition.md), which recovers the
  partition of the regression coefficients induced by the nonparametric
  Bayesian Lasso.
- The package now includes the functions
  [`coclust.probs()`](../reference/coclust.probs.md) and
  [`coclust.point()`](../reference/coclust.point.md), which compute and
  visualize the matrices of co-clustering probabilities and
  co-clustering point estimates, respectively.
- Other internal functionality improvements, including a better handling
  of numerical instabilities and memory management.
- GitHub version: [marinsantiago/bnplasso@4cf966b]()

## bnplasso 0.1.0

- Initial release with core functionality.
- Implementation as described in
  <https://doi.org/10.1080/10618600.2025.2572327>
- GitHub version: [marinsantiago/bnplasso@3c87169]()
