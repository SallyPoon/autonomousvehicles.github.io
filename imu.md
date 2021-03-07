---
layout: default
title: IMU
permalink: imu/
---

## Intertial Measurement Unit (IMU)
What exactly is an IMU you may ask? An IMU is a sensor that has an inbuilt accelerometer, gyroscope, and magenetometer and allows us to derive better relative position and orientation measurements for our robot. With this sensor we are able to measure Linear Acceleration, Angular Velocity, and sense Magnetic Fields and distortions in the X,Y, and Z axes. You can also derive the Roll, Pitch, and Yaw from these measurements.

IMUs are commonly used in most electronic devices and vehicles, such as robots, missiles, and even in your smartphone! 

![image](https://user-images.githubusercontent.com/43420182/110232018-eded1600-7ecf-11eb-9d36-b3df82ed6c85.png)

We utilized our IMU to primarily derive a Compass Heading (Yaw) for our robot so it could establish its orientation in a global context. 

## Sparkfun Openlog Artemis IMU & ROS Integration

The IMU sensor we used and integrated with was the Sparkfun Openlog Artemis IMU. Initially, we had begun a majority of our development on the Sparkfun Razor 9DoF IMU, which was quite seamless to interface with ROS and achieve good results. However, the Razor was retired midway in the quarter! So, we decided to move forward with the Artemis IMU, which was the upgraded released model. This IMU proved to be challenging to integrate into our robotic system which was developed in ROS (Robot Operating System). Yet, we were able to prevail after reaching out in the community and coming in contact with Fabrice Le Bars, who pointed us to his ROS package in development that would allow us to interface with this IMU! However, there were still quite a few issues down the line integrating onto our Jetson Single Board Computer, Flashing software, and building the right board definitions. Thankfully, we were able to overcome and learned to enjoy the process as this was our first real exposure with Hardware struggles as Data Science and Software focused students. We have developed a guide to help in this process and also contains information on calibration which we will delve into shortly.

## Calibration Analysis
It was crucial to calibrate our IMU to obtain the most accurate readings so that they could be relied upon by our robot's navigational stack. 
To do this we calibrated the accelerometer for gravitation force in all 3 axes at rest, the gyroscope noise levels at rest, and the magnetic disortions present in the environment at rest. The magnetometer provided the most difficulty in calibration. This is because there are often strong magnetic distortions caused by the metal hardware, magnetized components, motors, etc.. 

We analyzed 3 major calibration settings (after finetuning variety of parameters) for the Heading (Yaw) while driving a straight line path headed West (90 deg). The settings were calibrating acceloremeter+gyroscope, accel+gyro+standard magnetometer technique, and accel+gyro+extended magnetometer technique.
We found that the extended magnetometer calibration technique was a critical factor in providing accurate Heading estimates and reducing error, also giving us insight into how large of a factor magnetic distortions onboard our robot can intefere with our IMU data. 

--Insert Image of Test---

We then repeated this test except conducted a Half Arc 180 degree turn from West to East. The findings solidified our previous results by proper magnetometer calibration producing the least error. 

Here is a successful 180 degree turn with our Heading!

And now a successful 360 degree turn with our Heading!

## Mounting

We also tested different mounting strategies to see how it would affect our IMU readings. Our simple mount strategy was fairly naive with a ziptie and double sided electrical fastening the IMU into place. This mount gave us insight into the large error and bias that was produced due to the uneven pressure on the IMU and unsecure mount. This can be seen in the Linear Acceleration Y values and in the large fluctuations in the Yaw Heading values. 

Our second mount was more secure and utilized one of the mounting holes on the board. The error in the Linear Acceleration and Yaw was minimized, however the there was still occasional sway which negatively affected the accuracy of the readings. 

Overall the mounting strategies shined light on the extreme sensitivity of the IMU in its readings and the effects of the mount on these readings. Our next steps will be to test and integrate with our newly designed mount on our large 1/5 scale robot. 


## Noise Reduction Strategies

We researched several Noise Reduction approaches to attempt in migating the noise and bias that was affecting some of our IMU data readings, especially in Linear Acceleration. By applying Signal Processing techniques such as Low Pass Filter (which removes high frequency noise of a signal), Median Filter 

## Kalman Filter 

## OAK camera
