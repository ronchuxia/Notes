- Vehicle is given a sequence of 2D positions, i.e., waypoints, to follow.
- Vehicle knows where the given waypoints are in the vehicle’s frame of reference (the vehicle can localize itself).
- Goal is to follow these waypoints.

# Computing the Steering Angle
Follow the arc of a circle to reach the goal point.

![Arc](Figures/Pure%20Pursuit/Arc.png)

**ICR: Instantaneous Center of Rotation.**

![Radius](Figures/Pure%20Pursuit/Radius.png)

Radius:  
$$
r = \frac{L^2}{2|y|}
$$
Curvature:  
$$
\gamma = \frac{1}{r} = \frac{2|y|}{L^2}
$$
Steering angle should be proportional to the curvature.

# Picking a Goal Point
Option 1: Pick the closest waypoint just beyond the lookahead distance L. Then set L to be the distance to the waypoint.

Option 2: Interpolate between the two waypoints that sandwich the lookahead distance L.

# Tuning the Lookahead Distance
Tuning L will change the behavior of pure pursuit the most.

Small L:  
- Aggressive maneuver, oscillatory path.
- Accurate tracking.

Large L:  
- Less oscillatory path.
- Poor tracking.

NOTES:  
- The waypoints are a sequence of positions, and could also have a velocity component.
- The proportional gain can be tuned at different speeds.
