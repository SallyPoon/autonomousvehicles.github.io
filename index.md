# Welcome to Autonomous Vehicles!
#    Odometry and IMU Team


![IMG_1856-min](https://user-images.githubusercontent.com/13074631/110229215-95f8e400-7ebc-11eb-813c-96c579c45588.png)

## Introduction
Hello! We are Sally and Pranav and have completed our Data Science Capstone Senior Project by investigating the role and benefit of Odometry and IMU in Autonomous Vehicles. We will now introduce to you our Project and its Goals.

For a vehicle to successfully navigate istelf and even race autonomously, it is essential for the vehicle to be able localize itself within its environment. This is where Odometry and IMU data can greatly support the robot's navigational ability. Wheel Odometry provides useful measurements to estimate the position of the car through the use of wheel’s circumference and rotations per second. IMU, which stands for Interial Measurement Unit, is 9 axis sensor that can sense linear acceleration, angular velocity, and magnetic fields. Together, these data sources can provide us crucial information in deriving a **Position Estimate** (how far our robot has traveled) and a **Compass Heading** (orientation of the robot/where it's headed). 

While most navigation stacks rely on GPS or Computer Vision to achieve successful navigation, this leaves the robot vulnerable to unfavorable scenarios. For example, GPS is prone to lag and may be infeasible in unfamiliar terrain. Computer Vision approaches often depend heavily on training data and cannot always provide continouos and accurate orientation. Odometry and IMU readings are thus invaluable sources of sensing information that can easily complement and enhance navigational stacks in place to build more robust and accurate autonomous navigation models. 

Our aim is to calibrate, tune, and analyze Odometry and IMU data to provide most accurate Position Estimate, Heading, and data readings to achieve high performant autonomous navigation and racing ability.

## Goals
- Understanding of IMU and Odometry Sensor to help with reliable navigation and place within robot ecosystem.
- Guides for OLA Artemis IMU setup + calibration and Odometry tuning/analysis
- Calibration procedure of IMU sensor to ensure reliable measurements 
- Tuning procedure of Odometry to ensure accurate measurements
- Odometry derived Position Estimate
- IMU derived Primary Heading Estimate using fusion of accelerometer, gyroscope, and magnetometer readings
- IMU and Odometry data ready to be easily ingested by other subteams through ROS using package standard and custom topics
- IMU and Odometry data ready for fusion with GPS subteam within Kalman Filter if necessary for future advancement of robot localization
- Analyze data readings and Noise Reduction Strategies

## Want to read more?
[Odometry] - Read more on how sensors can calculate position!

[IMU] - 



![Alt Text](https://media.giphy.com/media/KcdCOCzmmfy0ZlzbXT/giphy.gif)

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [Odometry]: <https://sallypoon.github.io/autonomousvehicles.github.io/odometry/>
   [IMU]: <https://sallypoon.github.io/autonomousvehicles.github.io/imu/>
