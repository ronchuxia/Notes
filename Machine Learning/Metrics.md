# PSNR
**PSNR (Peak Signal-to-Noise Ratio)** measures pixel-wise intensity similarity.

Definition:
$$
\text{PSNR} = 10 \cdot \log_{10}\left(\frac{\text{MAX}^2}{\text{MSE}}\right)
$$
where $\text{MAX}$ is the maximum possible pixel value (e.g., 255) and
$$
\text{MSE} = \frac{1}{N} \sum_i (I_i - \hat{I}_i)^2
$$
is the mean squared error.