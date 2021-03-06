# dimreduce


An R package to perform (supervised) dimensionality reduction. The package contains essentially the techniques from the paper of Piironen and Vehtari (2018). The functions are very easy to use and require minimal input from the user.

I will add a vignette in the near future but below are some simple examples about how to use the package.


Installation
------------

```R  
if (!require(devtools)) {
  install.packages("devtools")
  library(devtools)
}
devtools::install_github('jpiironen/dimreduce')
```

Example
-------

```R
library(dimreduce)
library(ggplot2)

# load the features x and target values y for the prostate cancer data
data('prostate', package = 'dimreduce')

# try the difference dimension reductions 
dr0 <- spca(x) # pca
dr1 <- spca(x,y, nctot=2) # spca
dr2 <- ispca(x,y, nctot=2) # ispca

# choose one of the methods and visualize the data using the first two
# latent features
z <- predict(dr2,x)
ggplot() + geom_point(aes(x=z[,1], y=z[,2]), color=y+2)

# compute the p-values for the univariate relevances of each original feature
pval <- featscore.test(x,y)
qplot(pval) # should have uniform distribution if no relevant variables
sum(pval < 0.001) # number of variables with p-value below some threshold
```


References
------------

Bair, E., Hastie, T., Paul, D., and Tibshirani, R. (2006). Prediction by supervised principal components. *Journal of the American Statistical Association*, 101(473):119-137.

Neal, R. and Zhang, J. (2006). High dimensional classification with Bayesian neural networks and Dirichlet diffusion trees. In Guyon, I., Gunn, S., Nikravesh, M., and Zadeh, L. A., editors, *Feature Extraction, Foundations and Applications*, pages 265-296. Springer.

Piironen, J. and Vehtari, A. (2018). Iterative supervised principal components. To appear in *Proceedings of the 21st International Conference on Artificial Intelligence and Statistics (AISTATS)*. ([Preprint][piironenvehtari18])


[piironenvehtari18]: https://arxiv.org/abs/1710.06229

