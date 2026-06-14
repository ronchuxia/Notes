# Dead Reckoning
Dead reckoning calculates the current position of the car by using a previous position, and incorporate estimates of speed, heading, and elapsed time.

In our case:  
- Speed: ERPM is used to compute the longitudinal velocity.
- Heading: Servo angle is used to compute the steering angle.
- System: Kinematic bicycle model is used to compute the relative position.

Dead reckoning accumulates error over time.

# Bayes Rule
$$
P(B | A) = \frac{P(A|B) P(B)}{P(A)} \Rightarrow P(B|A, C_1, C_2, \dots C_n) = \frac{P(A|B, C_1, C_2, \dots, C_n) P(B| C_1, C_2, \dots, C_n)}{P(A|C_1, C_2, \dots, C_n)}
$$
# Recursive Bayes Filter
The recursive Bayes filter predicts system states $x$ based on sensor observations $o$ and control inputs $u$. Instead of a deterministic state, we approximates a distribution over state:  
$$
\text{Bel}(x_t) = P(x_t | o_t, u_t, o_{t-1}, u_{t-1}, \dots, o_1, u_1)
$$
Problem setting: Hidden Markov model.  
- Action model: $p(x_t | x_{t-1}, u_t)$.
- Sensor model: $p(o_t | x_t)$.

Recursive Bayes filter:  
- **Step 1: Prediction with control input (without observation).**
$$
\begin{aligned}
\bar{\text{bel}}(x_t) & = P(x_t | o_{1:t-1}, u_{1:t})\\
& = \int P(x_t | x_{t-1}, o_{1:t-1}, u_{1:t}) P(x_{t-1} | o_{1:t-1}, u_{1:t-1}) d(x_{t-1})\\
& = \int P(x_t | x_{t-1}, o_{1:t-1}, u_{1:t}) \text{bel}(x_{t-1}) d(x_{t-1})\\
& = \int P(x_t | x_{t-1}, u_t) \text{bel}(x_{t-1}) d(x_{t-1})  
\end{aligned}
$$  
- **Step 2: Correction with sensor observation.**
$$
\begin{aligned}
\text{bel}(x_t) & = P(x_t | o_{1:t}, u_{1:t})\\
& = \frac{P(o_t | o_{1:t-1}, x_t, u_{1:t}) P(x_t | o_{1:t-1}, u_{1:t})}{P(o_t | o_{1:t-1}, u_{1:t})}\\
& = \frac{P(o_t | x_t) P(x_t | o_{1:t-1}, u_{1:t})}{P(o_t | o_{1:t-1}, u_{1:t})}\\
& = \eta P(o_t | x_t) \bar{\text{bel}}(x_t)  
\end{aligned}
$$
Variants of recursive Bayes filter:  
- Kalman filter.
- Extended Kalman filter.
- Unscented Kalman filter.
- Particle filter.

# Particle Filter
Recursive Bayes filter involves multiplication and integration of two probability distributions. Particle filter represents distributions with a set of weighted samples (particles).

**Importance sampling:**  
To approximate a distribution $p(x)$, we draw a set of samples from another distribution $q(x)$:  
$$
x^{(i)} \sim q(x)
$$
And compute weights for each sample:  
$$
w^{(i)} = \frac{p(x^{(i)})}{q(x^{(i)})}
$$
Then the distribution $p(x)$ can be represented with the samples and their corresponding weights:  
$$
\hat p(x) = \sum_{i=1}^N w^{(i)} \delta_{x^{(i)}}(x)
$$
**Particle filter:**  
- **Step 1: Prediction with control input (without observation).**
	- For each particle i, sample:
		$$
		x^{(i)}_t \sim P(x_t | x^{(i)}_{t-1}, u_t)
		$$
	- This is equivalent to:
		$$
		x_t^{(i)} \sim \bar{\text{bel}}(x_t)
		$$
- **Step 2: Correction with sensor observation.**
	- For each particle i, compute weight:
		$$
		w^{(i)}_t = \eta P(o_t | x^{(i)}_t)
		$$
	- Normalize weights so they sum to 1.
	- Now the posterior can be represented by a set of weighted samples:
		$$
		S = \{<x^{(i)}_t, w^{(i)}_t> | \ i = 1, 2, \cdots, N\}
		$$
		$$
		\text{bel}(x) = \sum_{i=1}^N w^{(i)} \delta_{x^{(i)}}(x)
		$$
- **Step 3: Resample all particles with probability proportional to their weights.**
	- Resampling concentrates particles in high-probability regions by discarding low-weight particles and duplicating high-weight ones.
	- Now the posterior can be represented by a set of unweighted samples (including duplicates):
		$$
		S = \{<x^{(i)}_t> | \ i = 1, 2, \cdots, N\}
		$$
		$$
		\text{bel}(x) = \frac{1}{N} \sum_{i=1}^N \delta_{x^{(i)}}(x)
		$$
# Adaptive Monte Carlo Localization (AMCL)
**Adaptive Monte Carlo localization (AMCL)** is a localization algorithm that applies particle filter.  
- $x_t$: Robot pose.
- $u_t$: Odometry.
- $x^{(i)}_t = f(x^{(i)}_{t-1}, u_t) + \epsilon_t$: Apply dynamics and add noise.

AMCL has 2 key additions:  
- **KLD-sampling**: Dynamically adjusts the number of particles based on a statistical upper bound of the KL-divergence between the particle distribution and the true posterior. Fewer particles when confident, more particles when uncertain.
- **Recovery**: Injects random particles when the filter diverges.