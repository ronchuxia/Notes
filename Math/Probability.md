# Independence
Two random variables are independent when:
$$p(x, y) = p(x) p(y)$$

This is equivalent to
$$
p(x|y) = p(x)
$$
and
$$
p(y|x) = p(y)
$$

# Expectation
The expectation of a random variable is its average value.
$$
\mathbb E [X] = \int_x p(x) x dx
$$

# Variance
The variance of a random variable is the expectation of the squared distance to its expectation.
$$
\mathrm{Var}(X) = \mathbb E \left[ (X - \mathbb E[X])^2 \right]
$$

The standard deviation of a random variable is the square root of its variance.

# Covariance
The covariance of two random variables measures their linear relation.
$$
\mathrm{Cov}(X, Y) = \mathbb E[(X - \mathbb E[X])(Y - \mathbb E[Y])]
$$
- Positive covariance: When one variable increases, the other tends to increase.
- Negative covariance: When one variable increases, the other tends to decrease.

# Properties
Property 1:
$$
\mathrm{Var}(X) = \mathbb E[X^2] - (\mathbb E[X])^2
$$

Property 2:
$$
\mathrm{Cov}(X, Y) = \mathbb E[XY] - \mathbb E[X] \mathbb E[Y]
$$

Property 3:
$$
\mathbb E[X + Y] = \mathbb E[X] + \mathbb E[Y]
$$

Property 4:
$$
\mathbb E[aX] = a \mathbb E[X]
$$

Property 3 and property 4 are **linearity of expectation**.

Property 5:
$$
\mathrm{Var}(X + Y) = \mathrm{Var}(X) + \mathrm{Var}(Y) + 2\mathrm{Cov}(X, Y)
$$

Property 6:
$$
\mathrm{Var}(aX) = a^2 \mathrm{Var}(X)
$$

Property 7: 
If $X$ and $Y$ are independent,
$$
\mathbb E[XY] = \mathbb E[X] \mathbb E[Y]
$$

Property 8:
If $X$ and $Y$ are independent,
$$
\mathrm{Cov}(X, Y) = 0
$$

Property 9:
If $X$ and $Y$ are independent,
$$
\mathrm{Var}(X + Y) = \mathrm{Var}(X) + \mathrm{Var}(Y) 
$$

Property 10:
If $X$ and $Y$ are independent,
$$
\mathrm{Var}(XY) = \mathbb E[X^2] \mathbb E[Y^2] - (\mathbb E[X])^2 (\mathbb E[Y])^2
$$