## PID Controller

### Understanding the effects of Proportional (P), Integral (I) and Derivative (D) components of PID controller.

#### P - Proportional
***Proportional Control*** is a type of linear *feedback control system* in which a correction is applied to the controlled variable which is proportional to the crosstrack error (CTE). Since it accounts for the crosstrack error only, and not the speed and inertia of the vehicle, the corrective force isn't damped as it approaches the target value. Hence, it tends to overshoot, and make large, oscillating motions around the center.

#### D - Derivative
In this approach, the rate of change of the corrective force is damped as it approaches the target value, hence, reducing the overshooting considerably.

### I - Integral
The Integral (I) component accounts for steady state error (Eg. drifts) of the vehicle. This is done by using an integral component which is obtained by aggregating crosstrack error over time.

### Choosing the final hyperparameters
Because of the shortage of time, I did not get a chance to try out **Twiddle** for this project. Instead, I resorted to the manual approach. For me, the values for Proportional and Derivative components came out to around 0.1 and 0.9. The value for Integral component came out to be almost 0, possibly because the vehicle in the simular has an ideal behavior with zero steady state error (Eg. drift). I finally settled for (P, I, D) = (0.09, 0.000001, 0.9).

## Project
In the project:  
1. I have assigned the contructor arguments to class attributes Kp, Ki and Kd, which are hyperparameters for Proportional, Integral and Derivate components respectively.  
2. I have initialized the values for proportional, integral and derivate errors in the constructor.  
3. I have computed the i, d and p components respectively (in **UpdateError(double cte)**) as:    
	- i_error += cte  
	- d_error = cte - p_error  
	- p_error = cte  
4. I have computed the total error as: `-Kp * p_error - Ki * i_error - Kd * d_error`  
5. I have assigned the total error to steering_value for direct correction.
6. I have assigned the value for throttle_value based on range of absolute steering value.  

Code change: https://github.com/jmsktm/CarND-PID-Control-Project/commit/25edab4351b4707046c1b33dccd2453ce10ddf1c

## Video
Click to open on Youtube.  
[![PID Controller](https://i.ytimg.com/vi/F1LgjbBnEvA/hqdefault.jpg)](https://www.youtube.com/watch?v=F1LgjbBnEvA&feature=youtu.be)