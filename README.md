# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## The Model

States used for the model were - x coordinate of vehicle, y coordinate of vehicle, orientation, velocity, cross track error and orientation error. Actuators values calculated by controller were steer angle and throttle. All the states and coefficients of the polynomial drawn on center of the road were made input to the MPC solve function. This function gave throttle and steering value as the output. Actuator values were decided at each time step by MPC controller such that it minimizes the cost function defined. A vars vector was created which would store all the states and actuator values for all the points. Lowerbound and uperbound for values were fixed for states, actuators and contraint equations. CppAD::ipopt::solve function was used to get the optimum actuator values for each time step.

## Update Equations
* x = x + v*cos(psi)* dt
* y = y + v*sin(psi)* dt
* psi = psi - v*delta*dt/Lf
* v = v + a*dt

## Timestep Length and Elapsed Duration (N & dt)

N value was fixed at 10 and dt value at 0.1. Too large values of N made my vehicle to move erraticaly since my algorithm was trying to fit the far away points to reduce cost, and the closest point for which MPC actuator values are actually used was away from the fitted curve. Also too large N value makes the processing time larger and response slower, which created problems for my vehicle to take sharp turns. Too less value of N also made my vehicle to move erraticaly since model had no idea of the future state to give current actuator values.
dt value was fixed at 0.1. dt is the value after which actuator inputs are given while predicting future states. Too large value of dt created problems since vehicle would steer off after some time. So I tried to keep dt as small as possible. But too small dt made vehicle to run not very smoothly. So I finally decided dt value equal to 0.1.

## Polynomial Fitting 

To fit the polynomial firstly I computed waypoints in vehicles frame of refrence. Then I used polyfit function to fit the third order polynomial to the points. Waypoints in vehicles frame of reference were required for plotting line in the simulator.

## Model Predictive Control with Latency

Latency of 0.1 seconds was added to the system. To take its effect vehicle position 0.1 seconds in future was predicted using state model equations. This is because our model will give actuations to the vehicle after 0.1 seconds, so our initial state should be after 0.1 seconds to get the correct optimum control values. Since we calculated waypoints from vehicles frame of reference, future point of vehicle was also calculated from vehicle frame of reference. 
