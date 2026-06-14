![Scan Matching](Figures/Scan%20Matching/Scan%20Matching.png)

Premise: Most likely car position at Scan 2 is the position that gives the best overlap between the two scans.

Goal: Estimate the transformation to move one point cloud so that it is aligned with the other.

![Goal](Figures/Scan%20Matching/Goal.png)

Requirements:  
- Fast scan rate.
- Non-smooth, or heterogeneous, surfaces.

# SVD with Associations Known
If the correct correspondences are known, the correct relative rotation/translation can be computed directly.

Formal problem definition:  
- Given corresponding points:
$$
\mathbf y_n, \ \mathbf x_n, \ n = 1, 2, \cdots N
$$
- And weights (optional): 
$$
p_n, \ n = 1, 2, \cdots N
$$
- Find the parameters $R$, $\mathbf t$ of the rigid body transformation so that the squared error is minimized:
$$
R, \mathbf t = \arg\min_{R, \mathbf t}\sum ||\mathbf y_n - (R \mathbf x_n + \mathbf t)||^2 p_n
$$
![SVD with Associations Known](Figures/Scan%20Matching/SVD%20with%20Associations%20Known.png)

1. **Translation step**: Translate the point clouds so that their centroids sit at origin.
	1. Compute the mean of point sets.
		$$
		\mathbf y_0 = \frac{\sum \mathbf y_n p_n}{\sum p_n}, \ \mathbf x_0 = \frac{\sum \mathbf x_n p_n}{\sum p_n}
		$$

	2. Compute mean-reduced coordinates.
		$$
		\mathbf a_n = \mathbf y_n - \mathbf y_0, \ \mathbf b_n = \mathbf x_n - \mathbf x_0
		$$

2. **Rotation step**: Compute the rotation using SVD.
	1. Compute cross covariance matrix.
		$$
		H = \sum \mathbf a_n \mathbf b_n^T p_n
		$$

	2. Compute SVD.
		$$
		U D V^T = \text{svd}(H)
		$$

	3. Compute the rotation matrix.
		$$
		R = U V^T
		$$

	4. Compute the translation.
		$$
		\mathbf t = \mathbf y_0 - R \mathbf x_0
		$$
# SVD with Associations Unknown

![SVD with Associations Unknown](Figures/Scan%20Matching/SVD%20with%20Associations%20Unknown.png)

Iterative Closest Point (ICP):  
Repeat until convergence:  
1. Data association step: Compute correspondences from P to Q.
	1. For every $\mathbf p_i$ we search for the closest $\mathbf q_j$ to it.
2. Transformation step: 
	1. Translation step.
	2. Rotation step.

# Least Squares with Point-to-Point
In ICP, we minimize the squared distances between corresponding point pairs. However, this metric is sensitive to noise when correspondences are unknown.

**Point to projected point (point-to-point)** metric measures the distance as the distance to the **nearest point on the segment**.

![Point to Point](Figures/Scan%20Matching/Point%20to%20Point.png)

To optimize the point-to-point metric, ICP:  
1. Make an initial guess of the transform.
2. Iteratively improve the guess to reduce the metric.

# Least Squares with Point-to-Line/Plane
**Point-to-line** metric measures the distance as the distance to the **nearest line containing the segment**.

Least squares with point-to-line converges faster than least squares with point-to-point.