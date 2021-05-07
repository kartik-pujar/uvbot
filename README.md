# uvbot
This is a ROS package of a robot which can autonomously navigate in and out of every classroom and sanitize them parallely.

## Problem Statement 
Sanitizing the whole university uniformly, with equal priority to all places is a very time consuming and demanding process. Our aim is to automate this process with the help of robotics. 

## Solution

To build a robot which can autonomously navigate in and out of every classroom and sanitize them parallely.

## Introduction 

Presently, we aim to come up with a design for a robot that is capable of sterilizing surfaces and equipment using far-UVC bulbs. For autonomous navigation, the SLAM package is integrated. The use of automated disinfection equipment not only reduces human exposure to the virus but is also proving to be more rigorous and effective in decontaminating spaces.The robot is equipped with four far-UVC lamps around a central column on the top. The column is fixed on a mobile base where several sensors are integrated to detect motion plus position and to avoid obstacles. The robot can kill 99% bacteria and viruses.

## Background Research

A new study has shown that 99.9% of coronaviruses can be killed when exposed to far-UVC light. Far-UVC light also has a wavelength which is safe for humans.
Study shows 99.9% of coronaviruses killed by far-UVC light
Far-UVC light (222 nm) efficiently and safely inactivates airborne human coronaviruses


## IMPLEMENTATION 
Two motors with encoders along with two caster wheels are mounted on the bottom of a custom made metallic chassis. The Encoders are connected to a Jetson nano board which has a program running that takes the encoder values as input and outputs the odometry data. Encoders alone don't give accurate and stable odometry data, so the robot is equipped with a imu sensor.  The encoder data and imu data both are fused to give a filtered odometry data which is more accurate and stable data. This odometry data is used by the amcl package to localize the robot. The robot is also mounted with two lidars to obtain the obstacle data. This obstacle data is then used by the gmapping package to create a 2D map of the environment. The reason behind using two lidar is that one single lidar can't cover the whole 360 degree as the UV bulbs block the lidar. The data obtained from the two lidar is combined into one using a merge lidar value algorithm. As mentioned before this lidar is fed to a gmapping package which is a SLAM algorithm that uses an extended kalman filter to map the environment to give us a rough 2D map. In order to navigate, the Move base package is used. This package inputs the map of the environment and the goal to be reached and outputs the velocity of the two motors. These values are later given to arduino which is connected to motors to drive them using PWM signals. The goal is fed to the Move base package using the follow waypoints algorithm which basically takes multiple goals at a time and publishes them one by one creating a wave pattern In this manner the robot can navigate autonomously. As the robot navigates around the environment, the far-UVC bulbs mounted on top of the robot sanitize the surfaces. This far-UVC light ray not only kills the bacteria and viruses but also is not harmful to human skin. 



## Current Progress
Complete simulation of the robot is done on ROS and gazebo simulation tool and can be accessed at https://cutt.ly/uvrobot_video.
