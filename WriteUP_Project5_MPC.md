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

N value was fixed at 10 and dt value at 0.1. 
