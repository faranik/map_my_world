# map_my_world
This project is part of the Robotics Software Engineering scholar course offered at Udacity. It explores concepts like ROS, SLAM algorithm for mapping and localization problem,  RTAB-Map from ROS, which is an RGB-D, Stereo and Lidar Graph-Based SLAM implementation.

# Project Overview
Map My World! is a project exploring the creation of a 2D occupancy grid and 3D octomap from a simulated environment using a simple robot with the RTAB-Map package.
RTAB-Map (Real-Time Appearance-Based Mapping) is a popular solution for SLAM to develop robots that can map environments in 3D. 
For this project, we use the [rtabmap_ros](http://wiki.ros.org/rtabmap_ros)  package, which is a ROS wrapper (API) for interacting with RTAB-Map.
The project flow is as follows:
* Develop a package to interface with the rtabmap_ros package.
* Make the necessary changes to interface the robot with RTAB-Map.
* Ensure that all links are properly connected, naming is properly setup and topics are correctly mapped.
* When the robot is launched, teleop around the room to generate a proper map of the environment.
