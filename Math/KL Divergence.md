**KL divergence** measures the **proximity of two distributions p and q**.

# Definition
$$
D_\mathrm{KL}(p||q) = \mathbb E_{p(x)}\left[ \log \frac{p(x)}{q(x)} \right] = \int_x p(x) \log \frac{p(x)}{q(x)} dx
$$

# Property
**KL divergence is non-negative.**

# KL Divergence, Entropy and Cross Entropy
$$
D_\mathrm{KL}(p||q) = - H(p) + H(p, q)
$$

# Forward KL
In forward KL, p is the true distribution, q is the learned distribution.
$$
D_\mathrm{KL}(p_\mathrm{true} || q_\mathrm{learned})
$$

| x   | p(x) | q(x) | p(x) log(p(x)/q(x)) | effect on KL(p\|\|q) |
| --- | ---- | ---- | ------------------- | -------------------- |
| 1   | 0.4  | 0.4  | 0                   | no change            |
| 2   | 0.4  | 0.1  | 0.24                | big increase         |
| 3   | 0.1  | 0.4  | -0.06               | small decrease       |
| 4   | 0.1  | 0.1  | 0                   | no change            |

Forward KL insist on q having a good approximation for values that have high probability in p.

**Minimizing forward KL is equivalent to minimizing cross entropy, which is equivalent to maximum likelihood estimation.** [Entropy, Cross Entropy and Maximum Likelihood Estimation](Entropy,%20Cross%20Entropy%20and%20Maximum%20Likelihood%20Estimation.md)

# Backward KL
In backward KL, p is the learned distribution, q is the true distribution.
$$
D_\mathrm{KL}(p_\mathrm{learned} || q_\mathrm{true})
$$

Backward KL insists on p having a good approximation for values that have low probability in q.