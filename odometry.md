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
For the ERPM, we tried to find the best value for speed to erpm gain, which was only obtainable by constantly tuning and testing the value. To do this tuning, we took a tape measure and extended it by around two feet, put our car's back wheels at zero meters and drive straight. After driving straight, we can grab the distance by doing rostopic echo /vesc/odom/pose/pose/position/x. 


<figure>
<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224401-279e2c80-7e90-11eb-835d-0be1c28467dc.png">
  <figcaption>Start Point for ERPM Calibration</figcaption>
</figure>

<figure>
<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224450-8ebbe100-7e90-11eb-8694-f0b4eafd2b54.png">
  <figcaption>Midpoint Point for ERPM Calibration</figcaption>
</figure>

<figure>
<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224451-8fed0e00-7e90-11eb-94f0-f8575fbc1452.png">
  <figcaption>End Point for ERPM Calibration</figcaption>
</figure>

### ERPM Calibration Results
After this, if we got a distance that overshot, we decreased the speed to ERPM gain and if it undershot, we would increase the speed to ERPM gain. After testing the values of 4412, 4912, 5412, 3912, 3412, and 4012, we found that 4112 was the most accurate value with around a 0.0007 error from the actual position versus a 0.480117 ,0.118568, -0.178206, -042677, and -0.619709 error.

<img width="256" alt="linetable" src="https://user-images.githubusercontent.com/13074631/110224290-05f07580-7e8f-11eb-9f8e-bab3373bcc2f.png"> 

<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224239-b27e2780-7e8e-11eb-8acc-4b017871adc1.png"> <img width="423" alt="line3912" src="https://user-images.githubusercontent.com/13074631/110224240-b3af5480-7e8e-11eb-9246-6c95ecd0964a.png"> <img width="425" alt="line4112" src="https://user-images.githubusercontent.com/13074631/110224243-b4e08180-7e8e-11eb-92b5-91a96e4eeba1.png"> <img width="434" alt="line4612" src="https://user-images.githubusercontent.com/13074631/110224245-b6aa4500-7e8e-11eb-82ef-49d7956f5092.png"> <img width="424" alt="line5112" src="https://user-images.githubusercontent.com/13074631/110224248-b7db7200-7e8e-11eb-8dc4-2606a13e1617.png"> <img width="408" alt="line5612" src="https://user-images.githubusercontent.com/13074631/110224249-ba3dcc00-7e8e-11eb-965a-fa3e565ab30d.png">

## MushR Steering Angle Calibration

For this part, we followed a guide from MushR. To test the steering angle to server gain, we had to also have a tape measure and see the best value by running the car over and over. We had a tape measure go out to around 2.5m, then had set the back wheels to the beginning of the tape measure in a direction that makes it a T shape. To calculate what we needed as our arc, we needed to use

<figure>
<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224450-8ebbe100-7e90-11eb-8694-f0b4eafd2b54.png">
  <figcaption>Starting position for servo_to_erpm_gain Calibration</figcaption>
</figure>

<figure>
<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224778-700b1980-7e93-11eb-86e2-1385f220f519.png">
  <figcaption>Midturn for servo_to_erpm_gain Calibration/figcaption>
</figure>

<figure>
<img width="406" alt="line3412" src="https://user-images.githubusercontent.com/13074631/110224780-713c4680-7e93-11eb-80b3-795396c0aad5.png">
  <figcaption>Endpoint for servo_to_erpm_gain Calibration</figcaption>
</figure>

\
For our car the length is 0.475 and the maximum steering is 0.34. This ends up being around 2.44m. To do this test, we had to change the steering to erpm gain variable. The values had to be negative because if we set a positive steering to erpm gain, it would invert the turn. During our first tuning, we tried to do 0 however, we learned that if we set zero, it would not turn at all. During the test, our original value was 0.67 however we had to retune. This was because even though during our test it hit 2.44m, we realized that when graphing it with a constant speed, it would never hit that amount. Because of this, we decided to make our our tuning test.

## Improved Steering Angle Calibration

After finding that the MushR tuning test was not accurate for our needs, we decided to make our own test that uses our maximum distance value of 1.8m. For this test, we would turn the car each time and see how close it plots to 1.8m. To do this, we tried a steering to erpm gain of -0.5, which made over a full circle when we only did a half circle, showing that it was too much of a steering angle. After this, we through to increase the steering angle to -0.7 which preformed a little better but still made a full circle. We tried increasing it again to 0.8 servo to erpm gain to see how the change affects the circle because at the time, we did not know what caused it to run a full circle when we only ran a half circle. Our final try before researching more was 0.9 servo to erpm gain. Our final try before researching more was 0.9 servo to erpm gain.


<img width="443" alt="circle_0 5" src="https://user-images.githubusercontent.com/13074631/110224837-47cfea80-7e94-11eb-9e2b-707110270c76.png"> <img width="471" alt="circle_0 7" src="https://user-images.githubusercontent.com/13074631/110224839-4999ae00-7e94-11eb-8bd6-3035b1ca7d31.png"> <img width="462" alt="circle_0 8" src="https://user-images.githubusercontent.com/13074631/110224840-4c949e80-7e94-11eb-8026-493defa15708.png"> <img width="447" alt="circle_0 9" src="https://user-images.githubusercontent.com/13074631/110224841-4dc5cb80-7e94-11eb-9f23-a35f14017ffd.png">

After seeing that it was not giving the right predicted values, we decided to look into the file that predicts the odometry values. By going into the vesc to odom topic, we were able to find that the equation to calculate the odometry value is:

(data - steering to servo offset ) / steering to servo gain

current angular velocity = current speed * tan(current steering angle) / wheelbase
\newline

After reading the equation and testing values, we realized that the steering to servo gain directly changes the odometry prediction we would get. This means that if we increased the gain, it would start predicting a larger value and if we decreased the gain it would decrease the predicted value. Knowing this, we started changing our values again to try to perfect our odometry prediction.

For our second batch of tests, we tried starting with a -1.0 steering to erpm gain. When we did this we saw that it was close to half a circle however we wanted to ensure that by changing this servo to erpm gain to over -1, we would be getting closer to our intended half circle. Next, we tried a more extreme value of -10 and saw it only did a small arc, proving that by decreasing the servo to erpm gain we were decreasing the predicted arc value. Since we have proven the extremes of the erpm to servo gain values, we started honing into the right servo to erpm gain value. We tried -1.5 next however it still made too small of an arc. After this, we went changed the value to an erpm to servo gain of -1.2 which was very close however just shy of the amount we wanted the arc to be. The final value we tested was -1.1, which after testing gave an arc with only a 0.05m error.
<figure>
<img width="319" alt="circletable" src="https://user-images.githubusercontent.com/13074631/110224908-ebb99600-7e94-11eb-9b05-f5175710a003.png">

<img width="427" alt="circle1 0" src="https://user-images.githubusercontent.com/13074631/110224897-de9ca700-7e94-11eb-8d98-42e792217541.png"> <img width="437" alt="circle1 1" src="https://user-images.githubusercontent.com/13074631/110224898-e0ff0100-7e94-11eb-8b7d-41371c4bfdd3.png"> <img width="425" alt="circle1 2" src="https://user-images.githubusercontent.com/13074631/110224899-e2302e00-7e94-11eb-92e3-422e5283fcae.png"> <img width="421" alt="circle1 5" src="https://user-images.githubusercontent.com/13074631/110224901-e52b1e80-7e94-11eb-9470-4c339a4df8f9.png"> <img width="435" alt="circle10" src="https://user-images.githubusercontent.com/13074631/110224905-ea886900-7e94-11eb-81d8-d741a2fc6a54.png"> 

## Odometry Afterthoughts and Discussion!

The biggest issue we started with is that there was a problem with the directories of how we set our vesc file. During that time, we set the erpm to servo gain however it never changed the value when checking the erpm to servo gain parameter. To fix this issue, we had to go into forums such as the F110th and Mushr Slack and forums and ask for assistance. After discussing with them further, we found that how we set our directories was incorrect and it was not reading the vesc.yaml properly. We fixed how the VESC was reading the vesc.yaml and after that, we were able to test the erpm to servo gain.

Our first issue we started encountered was doing the steering angle tuning test and completing a 2.44m turn with a -0.67 servo to erpm gain gain. We considered this to be our final value and to validate, we started recording the predicted x and y values and graphing them to see if our tuning test was accurate. However, when we graphed the robot's pathing using the ERPM gain, we found that the odometry values overpredicted by double, showing a full circle pathing when we only drove half a circle. Because of this, we tried doing other values similar to out however we saw the same result mostly, showing that it drove half a circle. To try to understand this issue better, we went directly into the VESC node and looked at the equation used to calculate the odometry values and we found that based on the servo to erpm gain, if you decrease it even more, it will predict a smaller value, giving us a smaller arc.

Because of this, we had to retune the steering angle however since we made previous human errors, we used a constant speed of 1m/s rather than an unbounded speed. The problem however was that since our speed was bounded at 1m/s, we would never hit 2.44ms turning so we decided to tweak the test and make our own. For this new test, we wanted to make it so the distance we are trying to predict is 1.8m instead of using the kinematic model equation and tune based on that value. After this, we had to retest multiple new values such as -1.0 and -10 to prove our theory of the arc and half circle increasing and decreasing based on the servo to erpm gain. After proving our theory through testing, we decided to start honing in on the most accurate servo to erpm gain. Next we tried -1.5 which under predicted and then -1.2 which was only -0.1 off. Our final value was -1.1 with a -0.05 error.
