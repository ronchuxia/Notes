# Xavier
Xavier initialization keeps the scale of the **activations** and the gradients stable by initializing each weight with variance:
$$
\mathrm{Var}(W_{ij}) = \frac{2}{n_\text{in} + n_\text{out}}
$$

For an output before the activation:
$$
z_j = \sum_{i=1}^{n_\text{in}} x_i W_{ij} 
$$

Its variance:
$$
\begin{aligned}
\mathrm{Var}(z_j) & = \mathrm{Var} \left( \sum_{i=1}^{n_\text{in}} x_i W_{ij} \right)\\
& = \sum_{i=1}^{n_\text{in}}\mathrm{Var}(x_i W_{ij}) + \sum_{i \neq k}\mathrm{Cov}(x_i W_{ij}, x_k W_{kj})
\end{aligned}
$$

Assuming that
1. $x_i$ and $W_{ij}$ are independent.
2. $W_{ij}$ are i.i.d.
3. $\mathbb E[W_{ij}] = 0$.

Then
$$
\begin{aligned}
\mathrm{Cov}(x_i W_{ij}, x_k W_{kj}) & = \mathbb E[x_i x_k W_{ij} W_{kj}] - \mathbb E[x_i W_{ij}] \mathbb E[x_k W_{kj}]\\
& = \mathbb E[x_i x_k] \mathbb E[W_{ij}] \mathbb E[W_{kj}] - \mathbb E[x_i] \mathbb E[x_k] \mathbb E[W_{ij}] \mathbb E[W_{kj}]\\
& = 0
\end{aligned}
$$

Then the variance of the output
$$
\begin{aligned}
\mathrm{Var}(z_j) & = \sum_{i=1}^{n_\text{in}} \mathrm{Var}(x_i W_{ij}) + \sum_{i \neq k}\mathrm{Cov}(x_i W_{ij}, x_k W_{kj})\\
& = \sum_{i=1}^{n_\text{in}} \mathrm{Var}(x_i W_{ij})
\end{aligned}
$$

Assuming that 
1. $x_i$ and $W_{ij}$ are independent.
2. $\mathbb E[x_i] = 0$.
3. $\mathbb E[W_{ij}] = 0$.
4. $\mathrm{Var}(x_i) = \mathrm{Var}(x)$.
5. $\mathrm{Var}(W_{ij}) = \mathrm{Var}(W)$.

Then
$$
\begin{aligned}
\mathrm{Var}(x_i W_{ij}) & = \mathbb E[x_i^2 W_{ij}^2] - (\mathbb E[x_i W_{ij}]^2)\\
& = \mathbb E[x_i^2] \mathbb E[W_{ij}^2] - (\mathbb E[x_i])^2 (\mathbb E[W_{ij}])^2\\
& = \mathbb E[x_i^2] \mathbb E[W_{ij}^2]\\
& = \mathrm{Var}(x_i) \mathrm{Var}(W_{ij})\\
& = \mathrm{Var}(x) \mathrm{Var}(W)
\end{aligned}
$$

Note that assumption 2 is further based on the following assumption:
1. The input to the initial layer is normalized such that $\mathbb E \left[ x_i^{(0)} \right] = 0$.
2. **The activation function $f$ is an odd function** (e.g. tanh). 

Thus, the intermediate layers
$$
\mathbb E \left[ x_j^{(t)} \right] = \mathbb E \left[ f(z_j^{(t-1)}) \right] = - \mathbb E \left[ f(- z_j^{(t-1)}) \right]
$$

Assuming that
1. $W_{ij}$ is symmetric around 0.
2. $W_{ij}$ are i.i.d.
3. $x_i$ and $W_{ij}$ are independent.

 Then given any set of $x_i^{(t-1)}$, we can flip the sign of $z_j^{(t-1)}$ by flipping the signs of all $W_{ij}^{(t-1)}$, thus $z_j^{(t-1)} \overset{d}{=} -z_j^{(t-1)}$, where $\overset{d}{=}$ means "have the same distribution as", thus
$$
\mathbb E \left[ f(z_j^{(t-1)}) \right] = \mathbb E \left[ f(- z_j^{(t-1)}) \right]
$$

Thus
$$
\mathbb E[x_j^{(t)}] = 0
$$

Note that the result does not require any assumptions about the previous layer.

Note that assumption 4 is further based on the following assumption: The input to the initial layer is normalized such that $\mathrm{Var}(x_i^{(0)}) = 1$. For intermediate layers, the result does not require any assumptions about the previous layer.

Then the variance of the output
$$
\begin{aligned}
\mathrm{Var}(z_j) & = \sum_{i=1}^{n_\text{in}} \mathrm{Var}(x_i W_{ij})\\
& = n_\text{in} \mathrm{Var}(x) \mathrm{Var}(W)
\end{aligned}
$$

To keep the variance of the output and variance of the input the same:
$$
\mathrm{Var}(W) = \frac{1}{n_\text{in}}
$$

For the backward pass, to keep the variance of the gradient of the input and the variance of the gradient of the output the same:
$$
\mathrm{Var}(W) = \frac{1}{n_\text{out}}
$$

Xavier initialization makes a compromise of forward and backward pass:
$$
\mathrm{Var}(W) = \frac{2}{n_\text{in} + n_\text{out}}
$$

Note that Xavier initialization attempts to keep the variance unchanged between the input and the output **before** the activation. To keep the variance unchanged between the input and the output after the activation, we need to additionally assume that the activation is approximately linear (e.g. tanh near 0).

**Xavier uniform initialization** sets the initial weights of a neural network by sampling from a uniform distribution:
$$
W_{ij} \sim \mathcal U(-a, a)
$$
$$
a = \sqrt \frac{6}{n_\text{in} + n_\text{out}}
$$

**Xavier normal initialization** sets the initial weights of a neural network by sampling from a normal distribution:
$$
W_{ij} = \mathcal N(0, \sigma^2)
$$
$$
\sigma = \sqrt \frac{2}{n_\text{in} + n_\text{out}}
$$

# Kaiming
Kaiming initialization keeps the scale of the **pre-activation values** stable by initializing each weight with variance:
$$
\mathrm{Var}(W_{ij}) = \frac{2}{n_\text{in}}
$$

In Xavier initialization, we assume that the activation function $f$ is an odd function, which gives us $\mathbb E[x_i] = 0$. Kaiming initialization removes this assumption.

Assume that
1. $x_i$ and $W_{ij}$ are independent.
2. $\mathbb E[W_{ij}] = 0$.
3. $\mathbb E[x_i^2] = \mathbb E[x^2]$.
4. $\mathrm{Var}(W_{ij}) = \mathrm{Var}(W)$.

Thus
$$
\begin{aligned}
\mathrm{Var}(x_i W_{ij}) & = \mathbb E[x_i^2 W_{ij}^2] - (\mathbb E[x_i W_{ij}]^2)\\
& = \mathbb E[x_i^2] \mathbb E[W_{ij}^2] - (\mathbb E[x_i])^2 (\mathbb E[W_{ij}])^2\\
& = \mathbb E[x_i^2] \mathbb E[W_{ij}^2]\\
& = \mathbb E[x_i^2] \mathrm{Var}(W_{ij})\\
& = \mathbb E[x^2] \mathrm{Var}(W)
\end{aligned}
$$

Thus the variance of the output
$$
\begin{aligned}
\mathrm{Var}(z_j) & = \sum_{i=1}^{n_\text{in}} \mathrm{Var}(x_i W_{ij})\\
& = n_\text{in} \mathbb E[x^2] \mathrm{Var}(W)
\end{aligned}
$$

ReLU activation
$$
x^{(t)} = \max(0, z^{(t-1)})
$$

Thus
$$
\begin{aligned}
\mathbb E[x^2] & = \int_{-\infty}^{+\infty} p(x) x^2 dx\\
& = \int_{0}^{+\infty}p(x) x^2 dx\\
& = \int_{0}^{+\infty}p(z) z^2 dz\\
& = \frac{1}{2} \int_{-\infty}^{+\infty}p(z) z^2 dz\\
& = \frac{1}{2} \mathbb E[z^2]\\
& = \frac{1}{2} \mathrm{Var}(z)
\end{aligned}
$$

Thus the variance of the output
$$
\begin{aligned}
\mathrm{Var} (z_j) & = n_\text{in} \mathbb E[x^2] \mathrm{Var}(W)\\
& = \frac{n_\text{in}}{2} \mathrm{Var}(z) \mathrm{Var}(W)
\end{aligned}
$$

To keep the variance of the output and variance of the output in the previous layer the same:
$$
\mathrm{Var}(W) = \frac{2}{n_\text{in}}
$$

**Kaiming uniform initialization** sets the initial weights of a neural network by sampling from a uniform distribution:
$$
W_{ij} \sim \mathcal U(-a, a)
$$
$$
a = \sqrt \frac{6}{n_\text{in}}
$$

**Kaiming normal initialization** sets the initial weights of a neural network by sampling from a normal distribution:
$$
W_{ij} = \mathcal N(0, \sigma^2)
$$
$$
\sigma = \sqrt \frac{2}{n_\text{in}}
$$