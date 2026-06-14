Graph-based SLAM represent the SLAM problem as a graph:  
- **Node**: Robot poses (position + orientation) at different points in time.
- **Edge**: Spatial constraints between nodes, derived from sensor observations or odometry.

![Graph-Based SLAM](Figures/Graph-Based%20SLAM/Graph-Based%20SLAM.png)

![Loop Closure](Figures/Graph-Based%20SLAM/Loop%20Closure.png)

The process has two stages:  
- **Front-end**: 
	- As the robot moves, new nodes and edges are added. 
	- **Loop closure**: When the robot revisits a previously seen place, a new edge is added between the current node and the old node it recognizes. 
- **Back-end**: Once the graph is built, an optimization algorithm adjusts all node positions to minimize the total error across all edge constraints.

Loop closure corrects the error accumulated from dead reckoning.