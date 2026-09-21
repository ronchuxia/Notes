# Cross Entropy/Softmax Loss
## Definition
Input:
- $z$: logits.
- $y$: true class.

Convert logits to probability using **softmax** function:
$$
p_i = \text{softmax} (z)_i = \frac{e^{z_i}}{\sum_j e^{z_j}}
$$

Define **cross entropy/softmax loss** to be the negative log probability of the true class:
$$
l(z, y) = -\log p_{\text{y}} = \log \sum_j e^{z_j} - z_y
$$
## Interpretation
In information theory:
- $p(x)$: true distribution.
$$
p(x) = [0, \cdots, 1, \cdots, 0]
$$

- $q(x)$: predicted distribution.
$$
q(x) = \left[ \frac{e^{z_0}}{\sum_j e^{z_j}}, \cdots, \frac{e^{z_y}}{\sum_j e^{z_j}}, \cdots, \frac{e^{z_n}}{\sum_j e^{z_j}} \right]
$$

- $H(p, q)$: cross entropy.
$$
H(p, q) = − \sum_x p(x)\log(q(x))
$$

- $l(z, y)$: cross entropy/softmax loss.
$$
l(z, y) = H(p, q)
$$
## Gradient
$$
\frac{\partial l}{\partial z_i} = \frac{e^{z_i}}{\sum_j e^{z_j}} - 1\{ i = y\}
$$

# Binary Cross Entropy Loss
$$
L = -\left[y\log(p) + (1-y)\log(1-p)\right]
$$
Where:
- $y \in \{0,1\}$ is the true label.
- $p \in (0,1)$ is the predicted probability that $y = 1$.

