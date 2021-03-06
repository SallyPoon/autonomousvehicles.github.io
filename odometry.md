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
