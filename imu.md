---
layout: default
title: IMU
permalink: imu/
---

## Intertial Measurement Unit (IMU)
### What exactly is an IMU? 
An IMU is a sensor that has an inbuilt accelerometer, gyroscope, and magenetometer and allows us to derive better relative position and orientation measurements for our robot. With this sensor we are able to measure Linear Acceleration, Angular Velocity, and sense Magnetic Fields and distortions in the X,Y, and Z axes. 

IMUs are commonly used in most electronic devices and vehicles, such as jets, missiles, and even in your smartphone! 

<p float="left">
  <img src="https://user-images.githubusercontent.com/43420182/110232018-eded1600-7ecf-11eb-9d36-b3df82ed6c85.png" width="400" />
  <img src="https://user-images.githubusercontent.com/43420182/110261070-87b1d300-7f63-11eb-8931-92191b855f63.png" width="400" /> 
</p>

We utilized our IMU to primarily derive a Heading (Yaw) for our robot so it could establish its orientation in a global context. 
To derive the Roll, Pitch, and Yaw the following equations were utilized and implemented within ROS (robot operating system) on which robot's system was built: 

Roll = 180 * atan2(accelY, sqrt(accelX*accelX + accelZ*accelZ))/PI$

mag_x = magReadX*cos(pitch) + magReadY*sin(roll)*sin(pitch) + magReadZ*cos(roll)*sin(pitch)

mag_y = magReadY * cos(roll) - magReadZ * sin(roll)

Yaw = 180 * atan2(-mag_y,mag_x)/M_PI

## Sparkfun Openlog Artemis IMU & ROS Integration

The IMU sensor we used and integrated with was the Sparkfun Openlog Artemis IMU. Initially, we had begun a majority of our development on the Sparkfun Razor 9DoF IMU, which was quite seamless to interface with ROS and achieve good results. However, the Razor was retired midway in the quarter! So, we decided to move forward with the Artemis IMU, which was the upgraded released model. This IMU proved to be challenging to integrate into our robotic system which was developed in ROS (Robot Operating System). Yet, we were able to prevail after reaching out in the community and coming in contact with Fabrice Le Bars, who pointed us to his ROS package in development that would allow us to interface with this IMU! However, there were still quite a few issues down the line integrating onto our Jetson Single Board Computer, Flashing software, and building the right board definitions. Thankfully, we were able to overcome and learned to enjoy the process as this was our first real exposure with Hardware struggles as Data Science and Software focused students. We have developed a guide to help in this process and also contains information on calibration which we will delve into shortly.

<p align="center">
  <img align = "center" width="650" alt="Odomdf" src="https://user-images.githubusercontent.com/43420182/110232226-67d1cf00-7ed1-11eb-8146-504059e05f1c.png">
</p>

<p align="center">
  <img align = "center" width="300" alt="Odomdf" src="https://user-images.githubusercontent.com/43420182/110232147-f134d180-7ed0-11eb-8041-da3bb8130647.png">
</p>

## Mounting

We also tested different mounting strategies to see how it would affect our IMU readings. Our simple mount strategy was fairly naive with a ziptie and double sided electrical fastening the IMU into place. This mount gave us insight into the large error and bias that was produced due to the uneven pressure on the IMU and unsecure mount. This can be seen in the Linear Acceleration Y values and in the large fluctuations in the Yaw Heading values. 
### First Mount
<p align="center">
  <img align = "center" width="300" alt="Odomdf" src="https://user-images.githubusercontent.com/43420182/110269772-44625f00-7f79-11eb-9d59-98db66bdfddc.png">
</p>

![Screen Shot 2021-03-06 at 11 15 06 PM](https://user-images.githubusercontent.com/43420182/110269769-42000500-7f79-11eb-8d3f-fff0e136f3de.png)

### Second Mount
Our second mount was more secure and utilized one of the mounting holes on the board. The error in the Linear Acceleration and Yaw was minimized, however the there was still occasional sway which negatively affected the accuracy of the readings. 

<p float="left">
  <img src="https://user-images.githubusercontent.com/43420182/110270084-e97d3780-7f79-11eb-8d8a-5ed5fdb4774e.png" width="400" />
  <img src="https://user-images.githubusercontent.com/43420182/110270089-eb46fb00-7f79-11eb-8230-f51bd4755d96.png" width="400" /> 
</p>


![Screen Shot 2021-03-06 at 11 15 26 PM](https://user-images.githubusercontent.com/43420182/110270079-e6824700-7f79-11eb-9413-f038ffeda384.png)

Overall the mounting strategies shined light on the extreme sensitivity of the IMU in its readings and the effects of the mount on these readings. Our next steps will be to test and integrate with our newly designed mount on our large 1/5 scale robot. 

## Calibration Analysis
It was crucial to calibrate our IMU to obtain the most accurate readings so that they could be relied upon by our robot's navigational stack. 
To do this we calibrated the accelerometer for gravitation force in all 3 axes at rest, the gyroscope noise levels at rest, and the magnetic disortions present in the environment at rest. The magnetometer provided the most difficulty in calibration. This is because there are often strong magnetic distortions caused by the metal hardware, magnetized components, motors, etc.. 

We analyzed 3 best calibration settings (found through extendend testing of parameters in each condition) for the Heading (Yaw) while driving a straight line path headed West (90 deg). The settings were calibrating acceloremeter+gyroscope, accel+gyro+standard magnetometer technique, and accel+gyro+extended magnetometer technique. We found that the extended magnetometer calibration technique was a critical factor in providing accurate Heading estimates and reducing error, also giving us insight into how large of a factor magnetic distortions onboard our robot can intefere with our IMU data. 

### Straight Line Heading Test
<p align="center">
  <img align = "center" width=900" alt="Odomdf" src="https://user-images.githubusercontent.com/43420182/110232439-81bfe180-7ed2-11eb-9278-6cda91a422bf.png">
</p>

### Half Arc Heading Test
We then repeated this test except conducted a Half Arc 180 degree turn from West to East. The findings solidified our previous results by proper magnetometer calibration producing the least error. 

<p align="center">
  <img align = "center" width=900" alt="Odomdf" src="https://user-images.githubusercontent.com/43420182/110232546-1b878e80-7ed3-11eb-84be-53ee10b34764.png">
</p>

Now that we established and analyzed a proper calibration procedure, here were the results!

# 180 Degree Heading Turn 
Here is a successful 180 degree turn with our Heading from West to East (90 degrees to -90 degrees)!

![west_to_east_180](https://user-images.githubusercontent.com/43420182/110262143-91d5d080-7f67-11eb-88c9-a58c4daae19a.gif)

# 360 Degree Heading Turn 
And now a successful 360 degree turn with our Heading starting at West (90 degrees) and returning there!

![0_to_360](https://user-images.githubusercontent.com/43420182/110262222-dcefe380-7f67-11eb-9995-213f507cefe9.gif)


## Kalman Filter 

We utilized a Kalman Filter to fuse our IMU and Odometry readings to produce an enhanced position estimate and orientation for our robot. A Kalman filter is a 
used to obtain the best estimate of states (position in our case) through the combination of measurements from various sensors in order to mitigate noise The robot-localization package in ROS provides an implementation of an Extended Kalman Filter that has popular support and can be integrated into our navigation system. Surprisingly however, we found that the Kalman Filter we employed produced a slightly worse position estimate than one derived from our Odometry alone. This may be due to the linear acceleration slight bias that was inescapable due to the extreme sensitivity of the IMU sensor even after meticulous calibration. Thus, until we fuse our readings with ground truth GPS data, we will ignore the linear acceleration of the IMU within the Kalman Filter. Future work will be to implement and analyze an Unscented Kalman Filter, which is an advancement upon the base model and further investigate IMU noise compensation.

## Noise Reduction Strategies

We researched several Noise Reduction approaches to attempt in migating the noise and bias that was affecting some of our IMU data readings, especially in Linear Acceleration. By applying Signal Processing techniques such as Low Pass Filter (which removes high frequency noise of a signal), Median Filter (which smoothens a signal by applying the median across a sliding window), and Haar Wavelets (decomposition and reconstruction of signal to remove high frequency noise) we saw that while these approaches did mitigate the noise, it could not remedy the slight bias present in the IMU acceleration data even after meticulous calibration. We will next work to utilize an Allan Variance test to characterize the type of noise and bias instability. Then, we will further explore methods to compensate for the slight bias, especially in the acceleration readings.

## Discussion 

After calibrating and analyzing the Sparkfun OLA Artemis we were able to gain a strong understanding in several areas that will allow us to improve the accuracy of our IMU data and Heading derivation. Initially, we struggled with integration issues with our Sparkfun OLA Artemis IMU to our Jetson onboard computer and ROS. However, learning to reach out in the community and then give back has built our confidence in actively participating and growing within a larger network of robotocists. We then witnessed how the mounting setup can have a large effect on the IMU noise and reliability of data due to it being an extremely sensitive piece of hardware. We also saw the effects of the calibration procedure (which we developed a guide for!) and how strong of an negative influence the magnetic distortions onboard our robot can have on our Heading. Since the IMU is so sensitive, even after diligent calibration there is still a slight bias in acceleration values. The Kalman Filter that was primarily supposed to better our Position Estimate and Heading surprisingly performed worse most likely due to this, however led us to search for new ways to compensate for noise and bias.  After exploring popular signal processing techniques, we found some success, yet would like to next employ an Allan Variance test and further research to better address this. Finally, we would like to integrate to our larger 1/5 Rally Car and potentially race it at the Thunderhill Raceway Track in Northern California. 


Finally, we would like to thank our Professor, Jack Silberman, for giving us the opportunity to continue learning and devloping our data science and robotics knowledge!
 
 
Thanks for reading! 
