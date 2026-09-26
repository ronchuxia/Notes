# Sigmoid
$$
\sigma (x) = \frac{1}{1 + e^{-x}}
$$

# ReLU
Rectified Linear Unit.
$$
\mathrm{ReLU(x)} = \max(0, x)
$$

# Leaky ReLU
$$
f(x)= \begin{cases} 
x, & x\geq 0\\
\alpha x, & x<0
\end{cases}
$$
where $\alpha$ is a small positive constant, such as 0.01.
 
# GeLU
Gaussian Error Linear Unit.
$$
\mathrm{GeLU}(x) = x \Phi(x)
$$
where $\Phi(x)$ is the **standard normal cumulative distribution function**.

The standard normal cumulative distribution function is the probability that a standard normal random variable $Z$ is at most $x$:
$$
\Phi(x) = P(Z \leq x) = \int_{-\infty}^x \frac{1}{\sqrt{2\pi}} e^{-t^2/2} dt
$$

![](figures/gelu.png)


