---
layout: default
title: Odometry
permalink: odometry/
---

# Welcome to odometry!

## What is odometry?
Odometry is the use of motion sensors to estimate change over time. To do this, odometry requires the time, rotation per minute and steering angle. After this, we can calculate odometry by doing: 

![Screenshot_1](https://user-images.githubusercontent.com/13074631/110222668-b5761980-7e88-11eb-8d68-1daa2cbe491b.png)


Using this equation, the robot car can predict where it's location respective to it's last position. The goal of odometry is to get a estimate of where the robot has driven to respect to its starting point. This can be problematic alone as over time it may accumulate errors since it is an estimate of the car's position.


<img width="497" alt="Odomdf" src="https://user-images.githubusercontent.com/13074631/110222745-56fd6b00-7e89-11eb-85c8-12f0b9c599df.png">

## Calibration!!
### Where did we start?
#### You need on your car:
- Vedder Electronic Speed Controller

<img width="497" alt="Odomdf" src="https://user-images.githubusercontent.com/13074631/110222859-4ef1fb00-7e8a-11eb-8d6d-b055f8208cd5.jpg">

- Servo that has an encoder board

<img width="497" alt="Odomdf" src="https://user-images.githubusercontent.com/13074631/110222914-d17aba80-7e8a-11eb-9875-a7099eee5c53.png">

### What's next?
To increase the accuracy of our odometry readings, tuning has to be done on the VESC.yaml file to account both the steering and angle gain used in our equations. The equations being used are:


erpm (electrical rpm) = speed to erpm gain * speed (meters / second) + speed to erpm offset

servo value (0 to 1) = steering angle to servo gain * steering angle (radians) + steering angle to servo offset


### ERPM Calibration
For the ERPM, we tried to find the best value for speed to erpm gain, which was only obtainable by constantly tuning and testing the value. To do this tuning, we took a tape measure and extended it by around two feet, put our car's back wheels at zero meters and drive straight. After driving straight, we can grab the distance by doing rostopic echo /vesc/odom/pose/pose/position/x. After this, if we got a distance that overshot, we decreased the speed to ERPM gain and if it undershot, we would increase the speed to ERPM gain. After testing the values of 4412, 4912, 5412, 3912, 3412, and 4012, we found that 4112 was the most accurate value with around a 0.0007 error from the actual position versus a 0.480117 ,0.118568, -0.178206, -042677, and -0.619709 error.


<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224239-b27e2780-7e8e-11eb-8acc-4b017871adc1.png"> <img width="423" alt="line3912" src="https://user-images.githubusercontent.com/13074631/110224240-b3af5480-7e8e-11eb-9246-6c95ecd0964a.png"> <img width="425" alt="line4112" src="https://user-images.githubusercontent.com/13074631/110224243-b4e08180-7e8e-11eb-92b5-91a96e4eeba1.png"> <img width="434" alt="line4612" src="https://user-images.githubusercontent.com/13074631/110224245-b6aa4500-7e8e-11eb-82ef-49d7956f5092.png"> <img width="424" alt="line5112" src="https://user-images.githubusercontent.com/13074631/110224248-b7db7200-7e8e-11eb-8dc4-2606a13e1617.png"> <img width="408" alt="line5612" src="https://user-images.githubusercontent.com/13074631/110224249-ba3dcc00-7e8e-11eb-965a-fa3e565ab30d.png">

