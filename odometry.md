---
layout: default
title: Odometry
permalink: odometry/
---

# Welcome to odometry!

## What is odometry?
Odometry is the use of motion sensors to estimate change over time. To do this, odometry requires the time, rotation per minute and steering angle. After this, we can calculate odometry by doing: 

$$Position_{current} = {Position_{old} + Velocity * Time + \frac{1}{2} * Acceleration * Time^2}$$

Using this equation, the robot car can predict where it's location respective to it's last position. The goal of odometry is to get a estimate of where the robot has driven to respect to its starting point. This can be problematic alone as over time it may accumulate errors since it is an estimate of the car's position.
