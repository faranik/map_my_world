# map_my_world
This project is part of the Robotics Software Engineering scholar course offered at Udacity. It explores concepts like ROS, SLAM algorithm for mapping and localization problem,  RTAB-Map from ROS, which is an RGB-D, Stereo and Lidar Graph-Based SLAM implementation.

## Project Overview
Map My World! is a project exploring the creation of a 2D occupancy grid and 3D octomap from a simulated environment using a simple robot with the RTAB-Map package.
RTAB-Map (Real-Time Appearance-Based Mapping) is a popular solution for SLAM to develop robots that can map environments in 3D. 
For this project, we use the [rtabmap_ros](http://wiki.ros.org/rtabmap_ros)  package, which is a ROS wrapper (API) for interacting with RTAB-Map.
The project flow is as follows:
* Develop a package to interface with the rtabmap_ros package.
* Make the necessary changes to interface the robot with RTAB-Map.
* Ensure that all links are properly connected, naming is properly setup and topics are correctly mapped.
* When the robot is launched, teleop around the room to generate a proper map of the environment.

## Map My World!
We have everything ready to go. Launch the ROS nodes and let us start mapping.


First, launch the Gazebo world and RViz, spawn the robot in the environment:

 ``` roslaunch my_robot world.launch ```
Then, launch the teleop node:

``` rosrun teleop_twist_keyboard teleop_twist_keyboard.py ```
Finally, launch your mapping node:

``` roslaunch my_robot mapping.launch ```
Navigate your robot in the simulation to create map for the environment! When you are all set, terminal the node and you could find your map db file in the place you specified in the launch file. If you did not modify the argument, it will be located in the /root/.ros/ folder.

### Best Practices
You could start by lower velocity. Our goal is to create a great map with the least amount of passes as possible. Getting 3 loop closures will be sufficient for mapping the entire environment. You can maximize your loop closures by going over similar paths two or three times. This allows for the maximization of feature detection, facilitating faster loop closures! When you are done mapping, be sure to copy or move your database before moving on to map a new environment. Remember, relaunching the mapping node deletes any database in place on launch start up!

## Teleop Package
If you prefer to control your robot to help it explore the map, you would need to add the teleop node. You could use ros-teleop package to send command to the robot using keyboard or controller.

Clone the ros-teleop package to your src folder:
```
cd /home/workspace/catkin_ws/src
git clone https://github.com/ros-teleop/teleop_twist_keyboard
```
Build the package and source the setup script:
```
cd ..
catkin_make
source devel/setup.bash
```
Now you could run the teleop script as is described in the README file:
``
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

## Database Analysis
The rtabmap-databaseViewer is a great tool for exploring the rtab database when it is generated. It is isolated from ROS and allows for complete analysis of the mapping session.

This is how you will check for loop closures, generate 3D maps for viewing, extract images, check feature mapping rich zones, and much more!


Let’s start by opening our mapping database:

We can do this like so: rtabmap-databaseViewer ~/.ros/rtabmap.db

Once open, we will need to add some windows to get a better view of the relevant information, so:

Say yes to using the database parameters
View -> Constraint View
View -> Graph View
Those options are enough to start, as there are many features built into the database viewer!

Let’s talk about what you are seeing in the above image. On the left, you have your 2D grid map in all of its updated iterations and the path of your robot. In the middle you have different images from the mapping process. Here you can scrub through images to see all of the features from your detection algorithm. These features are in yellow. Then, what is the pink, you may ask? The pink indicates where two images have features in common and this information is being used to create neighboring links and loop closures! Finally, on the right you can see the constraint view. This is where you can identify where and how the neighboring links and loop closures were created.


You can see the number of loop closures in the bottom left. The codes stand for the following: Neighbor, Neighbor Merged, Global Loop closure, Local loop closure by space, Local loop closure by time, User loop closure, and Prior link.

When it comes time to design your own environment, this tool can be a good resource for checking if the environment is feature-rich enough to make global loop closures. A good environment has many features that can be associated in order to achieve loop closures.
