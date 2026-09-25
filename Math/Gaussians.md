# 1
Let: 
$$
X \sim \mathcal{N}(\mu_x, \sigma_x^2), \ Y \sim \mathcal{N}(\mu_x, \sigma_y^2)
$$

Sum of two Gaussians is a Gaussian: 
$$
X + Y \sim \mathcal{N}(\mu_x + \mu_y, \sigma_x^2 + \sigma_y^2)
$$

# 2
Let: 
$$
X \sim \mathcal{N}(\mu_x, \sigma_x^2)
$$
$$ 
Y = aX + b
$$

Affine function of a Gaussian is a Gaussian: 
$$
Y \sim \mathcal{N}(a\mu_x + b, a^2\sigma_x^2)
$$

# 3
Let: 
$$
X \sim \mathcal{N}(\mu_x, \sigma_x^2)
$$
$$
Z|X \sim \mathcal{N}(X, \sigma_z^2)
$$
i.e. $Z = X + \epsilon$, $\epsilon = \mathcal{N}(0, \sigma_z^2)$.  

Gaussian with a Gaussian mean has a Gaussian marginal: 
$$
Z \sim \mathcal{N}(\mu_x, \sigma_x^2 + \sigma_z^2)
$$

# 4
Let: 
$$
X \sim \mathcal{N}(\mu_x, \sigma_x^2)
$$
$$
Z | X \sim \mathcal{N}(aX + b, \sigma_z^2)
$$
i.e. $Z = g(X) + \epsilon$, $\epsilon \sim \mathcal{N} (0, \sigma_z^2)$.

Gaussian with a Gaussian mean has a Gaussian marginal: 
$$
Z \sim \mathcal{N}(a\mu_x + b, a^2\sigma_x^2 + \sigma_z^2)
$$
