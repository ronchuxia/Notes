# Subspace, Manifold and Nonlinear Set
## Subspace
A linear subspace is closed under linear combinations. 

If
$$
g(z)=Wz, \ z\in\mathbb R^d,
$$
then the output set
$$
\mathcal S=\{Wz:z\in\mathbb R^d\}
$$
is a linear subspace with dimension at most $d$. 

If
$$
g(z)=Wz+b,
$$
then the output set
$$
\mathcal S=\{Wz + b:z\in\mathbb R^d\}
$$
is an affine subspace.
## Manifold
A manifold is a set that may be curved globally but locally resembles a Euclidean space of fixed dimension. 

For example, the surface of a sphere is a two dimensional manifold embedded in three dimensional space.
## Nonlinear Set
The output of a nonlinear function is always a set, but it is not necessarily a manifold. It may contain folds, self intersections, sharp points, singularities, boundaries, or regions with different local dimensions.

# Natural Image Distribution
Natural images are represented in the full ambient pixel space, but their probability is believed to concentrate near a much smaller structured nonlinear set.

Image generation aims to seek a set $\mathcal S_d$ such that
$$
P\left(
\operatorname{distance}(X,\mathcal S_d)\leq\epsilon
\right)
\geq 1-\delta,
$$
where $d$ is the dimension of the set, $\epsilon$ is the allowed approximation error, and $\delta$ is the probability not captured near the set.
