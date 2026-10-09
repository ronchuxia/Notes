# Gradient
For a scalar-valued function $f: \mathbb R^n \rightarrow \mathbb R$, its gradient is the vector of the partial derivatives of $f$ with respect to each input:
$$
\nabla f(\mathbf x) = \left[ \frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n} \right]^T
$$

For a vector-valued function $f: \mathbb R^n \rightarrow \mathbb R^m$, the equivalence is its Jacobian.

# Subgradient
For a **convex** scalar-valued function $f: \mathbb R^n \rightarrow \mathbb R$, a vector $\mathbf g \in \mathbb R^n$ is a subgradient of $f$ at $\mathbf x$ if:
$$
f(\mathbf y) \geq f( \mathbf x) + \mathbf g^T (\mathbf y - \mathbf x) \quad \forall \mathbf y \in \mathbb R^n
$$

The subdifferential of $f$ at $\mathbf x$ is the set of all the subgradients:
$$
\partial f(\mathbf x) = \{ \mathbf g \in \mathbb R^n : f(\mathbf y) \geq f(\mathbf x) + \mathbf g^T (\mathbf y - \mathbf x)\ \forall y \}
$$

E.g. For $\mathrm{ReLU}(x) = \max(0, x)$:
$$
\partial \mathrm{ReLU}(x) = \begin{cases} \{0\} & x < 0 \\ [0, 1] & x = 0 \\ \{1\} & x > 0 \end{cases}
$$

# Jacobian
For a vector-valued function $f: \mathbb R^n \rightarrow \mathbb R^m$, its Jacobian is an $m × n$ matrix:
$$
J = \begin{bmatrix}
\frac{\partial f_1}{\partial x_1} & \dots & \frac{\partial f_1}{\partial x_n}\\
\vdots & \ddots & \vdots\\
\frac{\partial f_m}{\partial x_1} & \dots & \frac{\partial f_m}{\partial x_n}
\end{bmatrix}
$$

The chain rule: For a composition $h = g \circ f$, its Jacobian:
$$
J_h(\mathbf x) = J_g(f(\mathbf x)) J_f(\mathbf x)
$$

# Matrix Multiplication
Matrix multiplicaiton:
$$
A_{m \times n} = B_{m \times k} C_{k \times n}
$$
Gradient:
$$
(\nabla_B l)_{m \times k} = (\nabla_A l)_{m \times n} (C^T)_{n \times k}
$$
$$
(\nabla_C l)_{k \times n} = (B^T)_{k \times m} (\nabla_A l)_{k \times n}
$$

# Exponential Function
Define $e^x$ using the power series:
$$
e^x
=
1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\cdots
=
\sum_{n=0}^{\infty}\frac{x^n}{n!}.
$$

Differentiate each term:
$$
\frac{d}{dx}e^x
=
0+1+\frac{2x}{2!}+\frac{3x^2}{3!}+\cdots.
$$

The resulting series is the original series:
$$
\frac{d}{dx}e^x
=
1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\cdots
=
e^x.
$$

After establishing this result, we can derive the general rule. For a constant $p>0$:
$$
p^x=e^{x\ln p}.
$$
$$
\frac{d}{dx}p^x
=
e^{x\ln p}\ln p
=
p^x\ln p.
$$