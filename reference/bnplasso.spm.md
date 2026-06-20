# Fit sparse means models with a nonparametric Bayesian Lasso prior

This function fits sparse means models with a nonparametric Bayesian
Lasso prior (Marin et al., 2026).

## Usage

``` r
bnplasso.spm(
  y,
  prior = NULL,
  a = NULL,
  b = NULL,
  alpha = NULL,
  variance.prior.type = NULL,
  max.iters = 6000L,
  burn.in = 1000L,
  thin = 1L,
  polya = FALSE,
  float = FALSE
)
```

## Arguments

- y:

  Response variable. It should be a numeric vector size \\n\\.

- prior:

  A character string denoting which type of shrinkage prior should be
  employed. The options are either: (1) `"bnp.lasso"` which implements
  the nonparametric Bayesian Lasso as in Marin et al. (2025+), (2)
  `"b.lasso"` which implements the Bayesian Lasso as in Park and Casella
  (2008), or (3) `"b.adapt.lasso"` which implements the Bayesian
  adaptive Lasso as in Leng et al. (2014). Default is `"bnp.lasso"`.

- a:

  A positive scalar. If `prior = "bnp.lasso"`, it corresponds to the
  **shape** parameter in the gamma distribution used as a centering
  measure in the DP prior. If `prior = "b.lasso"`, it corresponds to the
  **shape** parameter in the gamma distribution used as prior in the
  shrinkage parameter, \\\lambda^{2}\\. If `prior = "b.adapt.lasso"`, it
  corresponds to the **shape** parameter in the gamma distribution used
  as prior in the shrinkage parameters, \\\lambda\_{j}^{2}\\, for
  \\j\in\\1,\dots,p\\\\. If not provided, the function will attempt to
  determine an appropriate value.

- b:

  A positive scalar. If `prior = "bnp.lasso"`, it corresponds to the
  **rate** parameter in the gamma distribution used as a centering
  measure in the DP prior. If `prior = "b.lasso"`, it corresponds to the
  **rate** parameter in the gamma distribution used as prior in the
  shrinkage parameter, \\\lambda^{2}\\. If `prior = "b.adapt.lasso"`, it
  corresponds to the **rate** parameter in the gamma distribution used
  as prior in the shrinkage parameters, \\\lambda\_{j}^{2}\\, for
  \\j\in\\1,\dots,p\\\\. If not provided, the function will attempt to
  determine an appropriate value.

- alpha:

  A positive scalar. If `prior = "bnp.lasso"`, it corresponds to the
  **concentration** parameter in the DP prior. If `prior = "b.lasso"` or
  `prior = "b.adapt.lasso"`, the argument is ignored. If not provided,
  the function will attempt to determine an appropriate value.

- variance.prior.type:

  A character string denoting whether the prior on the sampling variance
  should be an independent-type prior or a conjugate-type prior. See
  Moran et al. (2019) for details. The options are either
  `"independent"` or `"conjugate"`. If not provided, the function will
  attempt to determine an appropriate prior.

- max.iters:

  A positive integer corresponding to the total number of MCMC
  iterations. Default is 6000.

- burn.in:

  A positive integer corresponding to the number of draws discarded as
  burn-in. It should be smaller than `max.iters`. Default is 1000.

- thin:

  A positive integer specifying the period for saving samples. Default
  is 1.

- polya:

  logical. Whether a generalized Pólya urn sampling scheme or a blocked
  Gibbs sampling scheme should be employed to update the Dirichlet
  process mixture in the MCMC algorithm. If `TRUE`, a generalized Pólya
  urn sampling scheme would be used. Default is `FALSE`. Important: This
  argument is ignored if `prior != "bnp.lasso"`

- float:

  Logical. If `TRUE`, some internal routines will use single point
  precision for improved computational efficiency at the expense of
  numerical accuracy. If `FALSE`, double point precision will be used.
  Default is `FALSE`.

## Value

An object of S3 class, `'spmBayes'`, containing:

- `post.beta`: A matrix of size `n.draws`-by-`n.preds`, where each row
  is a posterior draw of the regression coefficients.

- `post.sigma2`: A vector of size `n.draws`, where each element is a
  posterior draw of the sampling variance.

- `post.tau2`: A matrix of size `n.draws`-by-`n.preds`, where each row
  is a posterior draw of the latent parameters \\\tau\_{j}^{2}\\.

- `post.lambda2`: A matrix of size `n.draws`-by-`n.preds`, where each
  row is a posterior draw of the shrinkage parameters
  \\\lambda\_{j}^{2}\\.

- `post.clust_idx`: If `prior = "bnp.lasso"`, a matrix of size
  `n.draws`-by-`n.preds`, where each row indicates to which cluster the
  regression coefficients belong to.

- `post.K`: If `prior = "bnp.lasso"`, a vector of size `n.draws`, where
  each element indicates the number of clusters in the corresponding
  MCMC iteration.

- `elapsed`: The elapsed (wall-clock) time of the MCMC sampler, in
  seconds.

- `a`: If `prior = "bnp.lasso"`, the **shape** parameter in the gamma
  distribution used as a centering measure in the DP prior. If
  `prior = "b.lasso"`, the **shape** parameter in the gamma distribution
  used as prior in the shrinkage parameter, \\\lambda^{2}\\. If
  `prior = "b.adapt.lasso"`, the **shape** parameter in the gamma
  distribution used as prior in the shrinkage parameters,
  \\\lambda\_{j}^{2}\\, for \\j\in\\1,\dots,p\\\\.

- `b`: If `prior = "bnp.lasso"`, the **rate** parameter in the gamma
  distribution used as a centering measure in the DP prior. If
  `prior = "b.lasso"`, the **rate** parameter in the gamma distribution
  used as prior in the shrinkage parameter, \\\lambda^{2}\\. If
  `prior = "b.adapt.lasso"`, the **rate** parameter in the gamma
  distribution used as prior in the shrinkage parameters,
  \\\lambda\_{j}^{2}\\, for \\j\in\\1,\dots,p\\\\.

- `alpha`: If `prior = "bnp.lasso"`, the **concentration** parameter in
  the Dirichlet process prior.

- `variance.prior.type`: Whether the variance on the sampling variance
  was an independent-type prior or a conjugate-type prior.

- `max.iters`: The total number of MCMC iterations.

- `burn.in`: The number of draws discarded as burn-in.

- `thin`: The period for saving draws.

- `n.obs`: The sample size.

- `n.preds`: The number of predictors.

- `n.draws`: The number of posterior draws after burn-in and thinning.

- `y`: Vector of responses.

- `loglik`: Matrix of size `n.draws`-by-`n.obs` with the log-likelihood
  of each observation at each MCMC iteration.

- `post.pred`: A matrix of size `n.draws`-by-`n.obs`, where each row is
  a draw from the posterior predictive distribution.

## References

C. Leng, MN. Tran, and D. Nott (2014), Bayesian adaptive Lasso. *Ann
Inst Stat Math*, 66:221-244

S. Marin, B. Long,and A. H. Westveld (2026), Adaptive Shrinkage with a
Nonparametric Bayesian Lasso.*Journal of Computational and Graphical
Statistics*, 35(2):854-864. doi:10.1080/10618600.2025.2572327

G. E. Moran, V. Rockova, and E. I. George (2019), Variance Prior Forms
for High-Dimensional Bayesian Variable Selection. *Bayesian Analysis*,
14(4):1091-1119.

T. Park, and G. Casella (2008), The Bayesian Lasso. *Journal of the
American Statistical Association*, 103(482):681-686.

## Author

Santiago Marin
