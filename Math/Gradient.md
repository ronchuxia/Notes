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