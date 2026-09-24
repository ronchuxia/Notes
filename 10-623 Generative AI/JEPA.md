Joint Embedding Predictive Architecture (JEPA) is a self supervised learning architecture that predicts representations rather than raw data.

Given context $x$ and a target $y$:
$$
\hat{z}_y = f(x)
$$
$$
z_y = g(y)
$$
$$
\mathcal{L} = \lVert \hat{z}_y - z_y \rVert^2
$$

$g$ encodes the target into a representation, while $f$ encodes the context and predicts that target representation.

Unlike next frame prediction, which is trained to reproduce every target pixel, JEPA is trained to match abstract features. This lets it ignore unpredictable details and learn semantic structure.