For a scalar function with a scalar input:
$$
f(x) = f(a) + f'(a) (x - a) + \frac{1}{2!} f''(a) (x - a)^2 + \cdots
$$

Start with a polynomial:
$$
P(x) = c_0 + c_1 (x - a) + c_2 (x - a)^2 + \cdots
$$
We choose coefficients $c_k$ such that:
$$
P(a) = f(a), \ P'(a) = f'(a), \ P''(a) = f''(a), \ \cdots
$$
Therefore,
$$
c_0 = f(a), \ c_1 = f'(a), \ c_2 = \frac{1}{2!} f''(a), \ \cdots
$$

For a scalar function with a vector input:
$$
f(\mathbf x) = f(\mathbf a) + \nabla f(\mathbf a)^T (\mathbf x - \mathbf a) + \frac{1}{2} (\mathbf x - \mathbf a)^T H_f(\mathbf a) (\mathbf x - \mathbf a) + O(||\mathbf x - \mathbf a||^3)
$$