# Data Structures and Algorithms for Robotics

1. to understand both discrete and continuous planning algorithms; A*, D*, anytime algorithms, RRTs, PRMs, state-lattices, path primitive approaches, etc. 
1. As for data structures; you should know graphs in detail - 
1. what are the trade-offs between adjacency matrices versus lists?, 
   + should you store edge weights up front or compute them on the fly?, 
   + should you prune out invalid edges or just nullify the weighting? 
1. Knowledge of trees, heaps, red-black trees, and hashmaps will certainly help.

## Algorithms

Since it is a mobile robot and they mention "motion planning," some relevant algorithms would likely include extensive use of Bayesian Filters. The Bayes Rule has some very interesting applications to robotics; it involves understanding what is going on here:

Here you are solving for a belief in some quantity, which could be a map or a location.  It's easier to understand if you break that above expression into 2 parts.
The first step is everything after, and including, the integral.  It basically means "Take what we already know and let's try to guess what it's going to look like in a little bit".
The second step is everything before the integral.  It basically means "Let's take our guess from last time, and make it a little bit better by reading our sensor data"

This simple algorithm has many very important extensions.  Since that job posting mentions moving across rough terrain, the robot needs a way to identify that terrain.  The relevant algorithms, which can all be derived from the above Bayes Rule (how cool is that!?) may be:
Linear Kalman Filters (algorithm for a linear system)
Extended Kalman Filters (algorithm for a non-linear system)
Unscented Kalman Filters (algorithm for a non-linear system)
Information Filters (performs better than the Kalman filter in step 2 above, slower in step 1, but does the same basic thing)
Histogram Filters (make a 2D, 3D, 4D, etc histogram of something)
Particle Filters (use Monte Carlo methods aka random stuff; most popular algorithm)

All of these are algorithms that can help solve the huge overarching SLAM problem, which may be a large part of that job posting.  SLAM is like a catch-22.  Consider this: when a robot tries to build a map, it uses information about where it is or localization.  When a robot tries to localize, it uses a map.  But how can you do either without the other?! That's what the SLAM problem is, and that's what all these algorithms help with.

Solving Half of SLAM Using A Particle Filter
[Here they work on the first half of SLAM: figuring out where the robot is.](https://youtu.be/AMX_OcweGv0)

Solving the Other Half of SLAM Using a Kalman Filter
[Here they work on the second half of SLAM: mapping.](https://youtu.be/IYXux_rjz4c)

Sensors
For some types of sensors, a PID (Proportional Integral Derivative Controller), may be ideal.  It is a controller that improves your sensor readings, see wikipedia: (http://en.wikipedia.org/wiki/PID...).

Text
If you're really interested in learning more about this, then the text Probabilistic Robotics (http://mitpress.mit.edu/catalog/...) by Sebastian Thrun is pretty much the be-all, end-all on mobile robotics. But keep in mind SLAM is probably only a portion of what the job posting is about; there's probably a bunch of kinematics, control systems, etc involved. 

The person who gets that job will probably have a solid foundation in all of these areas and then much more.  The people working at Boston Dynamics are pretty dang smart.
