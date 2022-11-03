# SDCND: Motion Planning and Decision Making for Autonomous Vehicles

## Requirement: 
In this project, the implementation of two of the main components of a traditional hierarchical planner: The Behavior Planner and the Motion Planner. Both will work in unison to be able to:
1. Avoid static objects (cars, bicycles and trucks) parked on the side of the road (but still invading the lane). The vehicle must avoid crashing with these vehicles by executing either a “nudge” or a “lane change” maneuver.
2. Handle any type of intersection (3-way, 4-way intersections and roundabouts) by STOPPING in all of them (by default)
3. Track the centerline on the traveling lane.

## Task to accomplish this:
* Behavioral planning logic using Finite State Machines - FSM
* Static objects collision checking.
* Path and trajectory generation using cubic spirals
* Best trajectory selection though a cost function evaluation. This cost function will mainly perform a collision check and a proximity check to bring cost higher as we get closer or collide with objects but maintaining a bias to stay closer to the lane center line.

To run this project in the workspace folder: 

Run on: New Terminal 1 window
```
1. su - student // Will say permission denied, ignore and continue 
2. cd /opt/carla-simulator/
3. SDL_VIDEODRIVER=offscreen ./CarlaUE4.sh -opengl
```

Run on: New Terminal 2 window
```
4. git clone https://github.com/udacity/nd013-c5-planning-starter.git // this line of code is only implemented once
5. cd nd013-c5-planning-starter/project
6 ./install-ubuntu.sh
7. cd starter_files/
8. git clone https://github.com/anthonymiglio/nd013-c4-motion-planning-and-decision-making.git
9. cmake .
10. make
11. cd .. // cd nd013-c5-planning-starter/project
12. ./run_main.sh // This will silently fail 
13. ctrl + C // to stop 
14. ./run_main.sh // run this again
15. Go to desktop mode to see CARLA

// If error bind is already in use, or address already being used
ps -aux | grep carla
kill id
```

The simulation on the CARLA platform shows that the ego vehicle can deviate from the three cars parked in the middle of the road and roadside and turn smoothly. Behavioral Planning makes the Follow Lane and Change Lane Left or Change Lane Right states. Then, the cubic spirals method, according ``plannig_param.h`` file, creates trajectories as the Number of paths parameter with the Number of points in the spiral, big enough to smooth the curve and diminish jerk. The selected motion trajectory for the ego vehicle is the one with the lower cost.

## Results:
Parameters selected: ``P_NUM_PATHS`` = 5 and ``P_NUM_POINTS_IN_SPIRAL`` = 16

<img src="/project/img/car1_path5_spiral16.png"/>
The Ego vehicle deviated from the car in the right lane in the middle of the road by Changing Lane Left.

<img src="/project/img/car2_path5_spiral16.png"/>
The Ego vehicle deviated from the car parked on the sidewalk by Changing Lane Right.

<img src="/project/img/car3_path5_spiral16.png"/>
The Ego vehicle deviated from the car in the left lane in the middle of the road by Changing Lane Right.