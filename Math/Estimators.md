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