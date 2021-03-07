---
layout: default
title: IMU
permalink: imu/
---

## Intertial Measurement Unit (IMU)
What exactly is an IMU you may ask? An IMU is a sensor that has an inbuilt accelerometer, gyroscope, and magenetometer and allows us to derive better relative position and orientation measurements for our robot. With this sensor we are able to measure Linear Acceleration, Angular Velocity, and sense Magnetic Fields and distortions in the X,Y, and Z axes. IMUs are commonly used in most electronic devices and vehicles, such as robots, missiles, and even in your smartphone! We utilized our IMU to primarily derive a Compass Heading for our robot so it could know its orientation in a global context. 

## Sparkfun Openlog Artemis IMU 

The IMU sensor we used and integrated with was the Sparkfun Openlog Artemis IMU. Initially, we had begun a majority of our development on the Sparkfun Razor 9DoF IMU, which was quite seamless to interface with ROS and achieve good results. However, the Razor was retired midway in the quarter! So, we decided to move forward with the Artemis IMU, which was the upgraded released model. This IMU proved to be challenging to integrate into our robotic system which was developed in ROS (Robot Operating System). Yet, we were able to prevail after reaching out in the community and coming in contact with Fabrice Le Bars, who pointed us to his ROS package in development that would allow us to interface with this IMU! However, there were still quite a few issues down the line integrating onto our Jetson Single Board Computer, Flashing software, and building the right board definitions. Thankfully, we were able to overcome and learned to enjoy the process as this was our first real exposure with Hardware struggles as Data Science and Software focused students. We have developed a guide to help in this process and also contains information on calibration which we will delve into shortly.


### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/SallyPoon/autonomousvehicles.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
