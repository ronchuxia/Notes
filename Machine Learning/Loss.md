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
l(p, y) = -\left[y\log(p) + (1-y)\log(1-p)\right]
$$
Where:
- $y \in \{0,1\}$ is the true label.
- $p \in (0,1)$ is the predicted probability that $y = 1$.

# L2 Loss
## Definition
Input:
- $f_\theta(x)$: model prediction.
- $y$: ground truth.

L2 loss:
$$L_2 = ||y - f_\theta(x)||_2^2$$
## Interpretation 1
If we model the conditional distribution $p_\theta(y | x)$ with a Gaussian with fixed variance:
$$
y | x \sim \mathcal N(f_\theta(x), \sigma^2)
$$

Then:
$$
- \log p_\theta(y | x) = \frac{1}{2 \sigma^2} ||y - f_\theta(x)||_2^2 + \mathrm{constant}
$$

Therefore, **minimizing L2 loss is equivalent to maximum likelihood estimation, under the model of a Gaussian with fixed variance**.

The model prediction $f_\theta(x)$ is the mean of the best Gaussian.
## Interpretation 2
For a fixed input $x$, L2 minimizes:
$$
\mathbb E[(Y - f_\theta(x))^2 | X = x]
$$

Decompose it as:
$$
\mathbb E[(Y - f_\theta(x))^2 | x] = \mathbb E[Y^2 | x] - 2 f_\theta(x) \mathbb E[Y | x] + (f_\theta(x))^2
$$

The minimum occurs at:
$$
f_\theta(x) = \mathbb E[Y | X = x]
$$

Note that this result holds no assumptions about the true distribution of the data. Therefore, whatever the true distribution of the data is, **L2 loss always predicts the mean of the true distribution**.

Basically, **whenever you use a Gaussian with fixed variance to fit a target distribution, MLE always puts the mean of that Gaussian at the mean of the target distribution**.

**This causes blurriness when the distribution of possible output images is multimodal.**