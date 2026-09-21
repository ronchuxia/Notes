# Introduction
GAN: generator + discriminator.

Example generator: DCGAN
- An inverted CNN with four fractionally-strided convolution layers.

Example discriminator: PatchGAN
- Look at each patch and predict whether it is real or fake.
- Helps avoid producing blurry images.
	- PatchGAN checks local sharpness.
	- Every image provides many training signals.

# Objective Functions
Generator $G_\theta (\mathbf z)$: generate an image.

Discriminator $D_\phi (\mathbf x)$: predict the probability of the image being real.

**Generator target:**
Minimize the probability of the generated image being classified as fake.
$$
\min_\theta \log \left( 1 - D_\phi ( G_\theta(\mathbf{z}^{(i)}) ) \right)
$$

**Discriminator target:**
Maximize the probability of the real image being classified as real, and the generated image being classified as fake.
$$
\max_\phi \log \left( D_\phi ( \mathbf{x}^{(i)} ) \right) + \log \left( 1- D_\phi ( G_\theta(\mathbf{z}^{(i)}) ) \right)
$$

This is essentially **binary cross entropy loss**.

# Scaling
Less diversity than diffusion: text-to-image needs more imagination.

# Signals of Unhealthy Training
**Discriminator accuracy reaches 100 percent** -> the generator gradient becomes very small (see below), the discriminator provides little information about how the generator should improve.

**Discriminator accuracy stays around 50 percent and hardly fluctuates** -> the generator gradient becomes very small, the discriminator is fooled by the generator and provides little information about how the generator should improve.

# Variant: Non Saturating Loss
GAN

The **non saturating loss** is a **generator loss** designed to avoid the **vanishing gradient** produced by the original generator objective.

Background: 
The original generator objective function is:
$$L_G = \log (1 - D(G(z)))$$
$$
D(G(z)) = \frac{1}{1 + e^{-a}}
$$
Where $a$ is the discriminator logit.

The gradient of the original generator objective with respect to the $a$:
$$\frac{\partial L_G}{\partial a} = \frac{1}{1 + e^{-a}} = D(G(z))$$

If the discriminator is too strong, $D(G(z)) = 0$, the generator gradient vanishes.

The **non saturating loss** is:
$$
L_G = - \log D(G(z))
$$

# Variant: R1 Penalty
Which Training Methods for GANs Do Actually Converge?
StyleGAN2

The **R1 penalty** regularizes the discriminator by **penalizing how sensitive its output is to small changes around real training samples**.

The **R1 penalty** is:
$$
R_1 = \frac{\gamma}{2} \mathbb E_{x \sim p_\text{real}} \left[ ||\nabla_x D(x)||_2^2 \right]
$$

The R1 penalty is added to the discriminator loss.