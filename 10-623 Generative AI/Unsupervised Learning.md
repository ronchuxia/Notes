**Unsupervised learning models the underlying distribution of the training data.**

Assumption: 
1. Data comes from distribution $p^*(x_0)$.
2. We choose a distribution $p_\theta (x_0)$ for which sampling $x_0 \sim p_\theta(x_0)$ is tractable.

Goal: learn $\theta$ s.t. $p_\theta(x_0) \approx p^*(x_0)$.

**Autoregressive LMs** and **latent variable models** are 2 popular unsupervised learning methods.

# Autoregressive Models
An autoregressive model defines a conditional distribution:
$$
p(x_t | x_1, \dots, x_{t-1}) \sim \text{Categorical}
$$

The joint distribution
$$
p_\theta(\mathbf x) = p_\theta(x_1) p_\theta(x_2 | x_1) \cdots p_\theta(x_t | x_1, \dots, x_{t-1})
$$
is tractable.

The learning target
$$
\theta = \arg\max_\theta \sum_{i=1}^N \log p_\theta(\mathbf{x}^{(i)})
$$
can be optimized directly.

Note that autoregressive models does not assume that token $x_t$ is only dependent on $x1, \dots, x_{t-1}$, it simply uses this conditional probability $p(x_t | x_1, \dots, x_{t-1})$ to model the whole joint distribution $p_\theta(\mathbf x)$.

# Latent Variable Models
A latent variable model defines a joint distribution over an observed variable $\mathbf x$ and an unobserved (latent) variable $\mathbf z$:
$$
p_\theta(\mathbf x, \mathbf z)
$$

It is often defined by:
$$
p_\theta(\mathbf z) \quad \text{and} \quad p_\theta (\mathbf x|\mathbf z)
$$

The marginal distribution
$$
p_\theta(\mathbf{x}) = \int_\mathbf{z} p_\theta(\mathbf{x} | \mathbf{z}) p_\theta(\mathbf{z}) d\mathbf{z}
$$
is often intractable for many latent variable models.
1. The integral often has no closed form.
2. Numerical integration scales poorly to high dimensions.
3. Most latent values contribute nothing to $p_\theta(\mathbf x)$ for a given $\mathbf x$.

Therefore, instead of directly maximizing $p_\theta(\mathbf x)$, different latent variable models use different methods:
1. GAN: playing minimax game.
2. VAE, diffusion: maximizing ELBO.