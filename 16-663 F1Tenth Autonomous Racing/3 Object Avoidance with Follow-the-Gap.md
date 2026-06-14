# Gaps

![Follow the Gap](Figures/Follow%20the%20Gap/Follow%20the%20Gap.png)

Lidar range == inf -> obstacle is very far -> possibly a gap.
 
Follow the furthest lidar range? No! Due to angular resolution of the lidar, the ray may pass through but the car may not.

**Gap: Series of at least n consecutive hits that pass some distance threshold t** (e.g. n=3, t=5.0).

# Naive Follow-the-Gap
1. Find the gaps (based on n & t).
2. Calculate the width of each gap.
3. Determine the widest gap.
4. Optional: Determine the “deepest” gap.

Steering direction:  
1. The middle of the widest gap.
2. The deepest ray of the widest gap.

Properties:  
- Works for holonomic robots (can turn in place).
- Works for non-holonomic robots in environments with sparse obstacles.
- Doesn’t consider car’s dimensions.
- Hard to determine t.

Why naive follow-the-gap won't work for non-holonomic robots in environments with dense obstacles.

![Naive](Figures/Follow%20the%20Gap/Naive.png)

The non-holonomic robot can't turn in place. It will collide with obstacles on its way to the target gap.

# Incorporating Affordances in Navigation
1. Represent the bot as a circle.
2. Inflate objects by $r_\text{rob}$.
3. Robot can now be represented as a point without any size.

**Tweak 1: At every timestep, cleverly avoid the nearest obstacle.**

![Tweak 1](Figures/Follow%20the%20Gap/Tweak%201.png)

1. Find nearest LIDAR point and put a "safety bubble" around it of radius $r_\text{rob}$.
2. Set all points inside bubble to distance 0. All nonzero points are considered ‘free space’.
3. Find maximum-length sequence of consecutive non-zeros among the ‘free space’ points (the max-gap).
4. Find the "best" point among this maximum-length sequence. (Naive: Choose the furthest point in free space, and set your steering angle towards it.)

Con: Changing direction frequently results in losing velocity.  
Better idea: if you're far from your closest obstacle, you don't need to immediately make a sharp turn to avoid it.

**Tweak 2: Disparity Extender.**

![Disparity Extender](Figures/Follow%20the%20Gap/Disparity%20Extender.png)

1. Find disparities in the lidar readings.
2. For each disparity, extend it half the width of the car plus some tolerance.
3. Find the direction with the farthest distance and head towards it.

**Tweak 3: Disparity Extender with Cornering.**
1. Scan all available LIDAR samples below -90 or above +90 degrees.
2. If any point is below a safe distance on the side of the car in the direction the car is turning, stop turning and just keep going straight.

Disparity Extender: Where it Fails.

![Disparity Extender Fail Case](Figures/Follow%20the%20Gap/Disparity%20Extender%20Fail%20Case.png)

**Tweak 4: Minimizing the wiggling.**

![Tweak 4](Figures/Follow%20the%20Gap/Tweak%204.png)

Set a max distance threshold, say threshold = 2m or 3m, then follow the center of the deepest gap instead of the deepest direction point.

# Other Reactive Methods
- Tangent Bug
- Artificial Potential Fields
