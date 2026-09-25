# Entropy
The entropy of a distribution $p$ is:
$$
H(p) = - \mathbb E_{x \sim p} [\log p(x)] = - \int_x p(x) \log p(x) dx
$$

It measures the inherent uncertainty of $p$.

# Cross Entropy
The cross entropy between distribution $p$ and $q$ is:
$$
H(p, q) = - \mathbb E_{x \sim p} [\log q(x)] = - \int_x p(x) \log q(x) dx
$$

It measures how surprised $q$ is by samples from $p$.

# Maximum Likelihood Estimation
Assumptions:
- Data $x$ comes from distribution $p(x)$.
- Data $x$ are IID.

Maximum likelihood estimation learns a distribution $q_\theta(x)$, such that:
$$
\begin{aligned}
\theta^* & = \arg\max \sum_{i=1}^N \log q_\theta(x_i)\\
& = \arg\min \left[ -\frac{1}{N} \sum_{i=1}^N \log q_\theta(x_i) \right] 
\end{aligned}
$$

The objective is a [Monte Carlo Estimation](Monte%20Carlo%20Estimation.md) of $H(p, q)$.
$$
\hat H(p, q) = - \frac{1}{N} \sum_{i=1}^N \log q_\theta(x_i)
$$

Therefore, **maximum likelihood estimation approximately minimizes the cross entropy**.

# KL Divergence, Entropy and Cross Entropy
$$
D_\mathrm{KL}(p||q) = - H(p) + H(p, q)
$$
[KL Divergence](KL%20Divergence.md)