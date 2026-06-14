# SLAM Overview
**Simultaneous Localization and Mapping (SLAM)** is the problem of building a map while simultaneously determining your position in that map.

The chicken-and-egg problem:  
- To localize, you need a map. 
- To build a map, you need to localize.  
SLAM incrementally solves both problems at the same time.

![SLAM Overview](Figures/Hector%20SLAM/SLAM%20Overview.png)

# Occupancy Grid Mapping
Occupancy grid mapping represents the map as a grid of cells.

Assumptions:  
- All cells are independent.
- Given the true occupancy, the current measurement is independent of past measurements.

Measurement:  
- $m = 1$: Lidar hit.
- $m = 0$: No occlusion.

Map cell occupancy:  
- $z = 1$: Occupied.
- $z = 0$: Unexplored.
- $z = -1$: Free.

Measurement model: $p(m | z)$.

Log odd of a cell being occupied, given the measurements:  
$$
\log \text{odd}_t = \log \frac{p(z = 1 | m_{1:t})}{p(z = 0 | m_{1:t})}
$$
According to Bayes rule and the above assumptions:  
$$
\begin{aligned}
\frac{p(z = 1 | m_{1:t})}{p(z = 0 | m_{1:t})} & = \frac{p(m_t | z = 1, m_{1:(t-1)}) p(z = 1 | m_{1:(t-1)}) / p(m_t | m_{1:(t-1)})}{p(m_t | z = 0, m_{1:(t-1)}) p(z = 0 | m_{1:(t-1)}) / p(m_t | m_{1:(t-1)})}\\
& = \frac{p(m_t | z = 1, m_{1:(t-1)}) p(z = 1 | m_{1:(t-1)})}{p(m_t | z = 0, m_{1:(t-1)}) p(z = 0 | m_{1:(t-1)})}\\
& = \frac{p(m_t | z = 1) p(z = 1 | m_{1:(t-1)})}{p(m_t | z = 0) p(z = 0 | m_{1:(t-1)})}\\
\end{aligned}
$$  
Therefore, the map update rule:  
$$
\log \text{odd}_t = \log \text{odd}_{t-1} + \log \frac{p(m_t | z = 1)}{p(m_t | z = 0)}
$$
Threshold the cell values by upper/lower limit to avoid being completely certain.

# Hector Mapping
Hector mapping is a SLAM algorithm that does not require odometry. It uses **occupancy grid mapping** as its map representation.

**Scan matching via Gaussian-Newton optimization**  
Hector mapping estimates robot pose by matching lidar scan with occupancy grid:  
$$
\xi^* = \arg\min_\xi \sum_{i=1}^n [1 - M(S_i(\xi))]
$$
- $S_i(\xi)$: Impact coordinate of ith Lidar point in world frame.
- $M(S_i(\xi))$: Map value at coordinate given by $S_i(\xi)$.

Hector mapping use **Gaussian-Newton method** to optimize the target above.

**Multi-Resolution map alignment**  
Hector mapping maintains a **map pyramid**. When a new Lidar scan comes, hector mapping first matches it with the coarse map to estimate an initial pose, then it matches it with the fine map to refine the accuracy.