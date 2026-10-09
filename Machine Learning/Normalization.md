Normalization keeps numbers at a stable scale.

Its effects can be modeled by the neural network itself. But it makes training much easier, faster and more stable.

# Batch Normalization
Batch normalization **normalizes each feature independently** across all activations/tokens in the same batch.

For all features $x_{ij}$, where i identifies the activation/token, and j identifies the feature:
$$
\mu_j = \frac{1}{m} \sum_{i=1}^m x_{ij}
$$
$$
\sigma_j^2 = \frac{1}{m} \sum_{i=1}^m (x_{ij} - \mu_j)^2
$$
$$
y_{ij} = \gamma_j \frac{x_{ij} - \mu_j}{\sqrt{\sigma_j^2 + \epsilon}} + \beta_j
$$

Permanently forcing every feature to have zero mean and unit variance could restrict the network, therefore, a learnable weight $\gamma_i$ and bias $\beta_i$ are introduced to let the network choose a useful scale and center while retaining the optimization benefits of normalization.

![batch-norm-2d](figures/batch-norm-2d.png)

**The result is equivalent to adjusting the center and scale of each feature independently.**

Note that batch normalization uses the **empirical variance** instead of the sample variance. (It doesn't make much difference.) Meanwhile, it keeps a **running average of the sample variance** as an estimate of the population variance.
$$
S_j^2 = \frac{m}{m - 1} \sigma_j^2
$$
$$
{S_\text{run}}_j^2 \leftarrow (1 - \alpha) {S_\text{run}}_j^2 + \alpha S_j^2
$$

It also keeps a running average of the sample mean.
$$
{\mu_\text{run}}_j \leftarrow (1 - \alpha) {\mu_\text{run}}_j + \alpha \mu_j
$$

During inference, it uses the **stored running mean and variance**.

# Layer Normalization
Layer normalization **normalizes each activation/token independently** across its features.

For all features $x_{ij}$, where i identifies the activation/token, and j identifies the feature:
$$
\mu_i = \frac{1}{d} \sum_{j=1}^d x_j
$$
$$
\sigma_i^2 = \frac{1}{d} \sum_{j=1}^d (x_j - \mu_i)^2
$$
$$
y_{ij} = \gamma_j \frac{x_{ij} - \mu_i}{\sqrt{\sigma_o^2 + \epsilon}} + \beta_j
$$

Note that the learned weight $\gamma_j$ and bais $\beta_j$ are still **per feature**.

![layer-norm-2d](figures/layer-norm-2d.png)

Note that in the 2d example, the vector after layer norm is either $[0, 0]$, $[1, -1]$ or $[-1, 1]$. Some information may be lost due to feature correlation in layer normalization.

![](figures/layer-norm-3d.png)

If $d$ is the size of the input vector, $k$ is the dimension of the input set $S$, $k \leq d$:
$$
\text{dim} \ {\text{LN}(S)} \leq \min(k, d-2)
$$

Layer normalization does not have running statistics.

# AdaLN
AdaLN is a variant of layer normalization whose scale and shift depend on a **conditioning input**.
$$
y(\mathbf x, \mathbf c) = \gamma(\mathbf c) \frac{\mathbf x - \mathbf \mu(\mathbf x)}{\sqrt{\sigma^2(\mathbf x) + \mathbf \epsilon}} + \beta(\mathbf c)
$$
