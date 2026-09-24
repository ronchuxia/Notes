# Definition
Goal: Estimate the expectation of a function $f$ of a random variable $\mathbf X \sim P(\mathbf X)$:
$$
\phi = \mathbb E_{\mathbf x \sim p(\mathbf x)} [f(\mathbf x)] = \int_\mathbf x p(\mathbf x) f(\mathbf x) d \mathbf x
$$

Monte Carlo Estimation: Approximate the expectation by drawing $S$ samples from $p$ and computing the average of the function $f$ on the samples:
$$
\hat \phi = \frac{1}{S} \sum_{s = 1}^S f(\mathbf x^{(s)})
$$

# Properties
1. Monte Carlo estimation is an **unbiased** estimator:
$$
\mathbb E[\hat \phi] = \mathbb E \left[ \frac{1}{S} \sum_{s=1}^S f(\mathbf x^{(s)}) \right] = \frac{1}{S} \sum_{s=1}^S \mathbb E [f(\mathbf x^{(s)})] = \phi
$$
2. The variance of $\hat \phi$ shrinks as the number of sample grows:
$$
\begin{aligned}
\mathrm{Var}(\hat \phi) & = \mathrm{Var} \left( \frac{1}{S} \sum_{s = 1}^S f(\mathbf x^{(s)}) \right)\\
& = \frac{1}{S^2} \sum_{s = 1}^S \mathrm{Var} \left( f(\mathbf x^{(s)}) \right)\\
& = \frac{1}{S} \mathrm{Var}(f(\mathbf x))
\end{aligned}
$$
