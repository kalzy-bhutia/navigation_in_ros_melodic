# navigation_in_ros
[![Build Status](https://travis-ci.org/sanjaythakur/navigation_in_ros.svg?branch=master)](https://travis-ci.org/sanjaythakur/navigation_in_ros)

## What does this repository do?
It is a demonstration of using ROS navigation stack with a custom made robot on Gazebo.

## How to use this repository?
#### Mapping
1. Launch the environment
There are two environments. So either run 
```roslaunch navigation_in_ros environment.launch environment:=1```
or
```roslaunch navigation_in_ros environment.launch environment:=2```
This will launch the gazebo GUI and rviz along with some other nodes.
2. Launch gmapping
```roslaunch mybot_navigation gmapping_demo.launch```
3. Launch keyboard control
```roslaunch navigation_in_ros keyboard_teleop.launch```