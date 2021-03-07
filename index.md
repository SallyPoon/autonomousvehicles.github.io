# Welcome to Autonomous Vehicles!
#    Odometry and IMU Team


![IMG_1856-min](https://user-images.githubusercontent.com/13074631/110229215-95f8e400-7ebc-11eb-813c-96c579c45588.png)

## Introduction
When building systems for autonomous vehicle racing and driving, it is critical for the robot to localize itself within the environment it is navigating. Robot localization comprises of the robot being able to derive its current path and its heading for future motion estimation. Popular approaches often involve using GPS data solely and computer vision sensing. However, relying heavily on GPS coordinates or LiDar in open outdoor environments can lead to several issues. GPS is prone to lag and may be infeasible in harsher and unfamiliar terrain, resulting in loss of accuracy in tracking by failing to produce necessary positional information. Computer Vision approaches often depend heavily on training data and cannot always provide continouos and accurate orientation. Our problem investigates using IMU and Odometry sensors to aid in this mission by providing relevant data, position estimates, and vehicle heading in cases when GPS and other mapping are not reliable, or to supplement these approaches. IMU (Inertial  Measurement  Unit) provides linear acceleration, angular velocity, and magnetic force sensing ability through the use of accelorometers, gyroscopes, and occasionally magnetometers.  Wheel Odometry  also provide  useful  measurements  to  estimate the  position  of  the  car  through  the use of the wheel’s circumference and rotations per second. Together, these  sensors provide relevant and invaluable data that can be fused to obtain a primary heading and position estimate for the robot. Furthermore, these sensors can be fused with navigation and obstacle avoidance systems already in place to build more robust and accurate autonomous navigation models.

## Goals
- Understanding of IMU and Odometry Sensor to help with reliable navigation and place within robot ecosystem.
- Guides for OLA Artemis IMU setup + calibration and Odometry tuning/analysis
- Calibration procedure of IMU sensor to ensure reliable measurements 
- Odometry derived position estimation
- IMU derived Primary Heading estimate using fusion of accelerometer, gyroscope, and magnetometer readings
- IMU and Odometry data ready to be easily ingested by other subteams through ROS using package standard and custom topics
- IMU and Odometry data ready for fusion with GPS subteam within Kalman Filter if necessary for future advancement of robot localization
- Integrating, calibrating, and testing IMU on the real robot
- Tuning the car for accurate odometry readings


## Want to read more?
[Odometry] - Read more on how sensors can calculate position!

[IMU] - 



![Alt Text](https://media.giphy.com/media/KcdCOCzmmfy0ZlzbXT/giphy.gif)

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [Odometry]: <https://sallypoon.github.io/autonomousvehicles.github.io/odometry/>
   [IMU]: <https://sallypoon.github.io/autonomousvehicles.github.io/imu/>
