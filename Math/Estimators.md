# Unbiased
If an estimator $\hat \theta$ estimates a parameter $\theta$, it is unbiased when:
$$
\mathbb E[\hat \theta] = \theta
$$

e.g. For samples $X_i$ from a population with mean $\mu$, the sample mean
$$
\bar X = \frac{1}{n} \sum_{i=1}^N X_i
$$
is an unbiased estimator of the population mean $\mu$ because
$$
\mathbb E[\bar X] = \frac{1}{n} \sum_{i=1}^N \mathbb E[X_i] = \mu 
$$

# Consistent
If an estimator $\hat \theta$ estimates a parameter $\theta$, it is consistent when:
$$
\hat{\theta}_n \xrightarrow{p} \theta \quad \text{as} \quad n \rightarrow \infty
$$

# Standard Error
The standard error is the standard deviation of an estimator.
$$
\mathrm{SE}(\hat \theta) = \sqrt{\mathrm{Var}(\hat \theta)}
$$

# Sample Mean
The sample mean is the average of the values in a sample.
$$
\bar X = \frac{1}{n} \sum_{i=1}^n X_i
$$

Property 1: It is an **unbiased** estimator of the population mean.
$$
\mathbb E[\bar X] = \mathbb E[X]
$$

Property 2: If the samples are i.i.d with variance $\sigma^2$, its variance is
$$
\mathrm{Var(\bar X)} = \frac{\sigma^2}{n}
$$

# Sample Variance
The sample variance is:
$$
S^2 = \frac{1}{n-1} \sum_{i=1}^n (X - \bar X)^2
$$

Property 1: It is an unbiased estimator of the population variance.
$$
\mathbb E [S^2] = \mathrm{Var}(X)
$$