# navigation_in_ros_melodic
[![Build Status](https://travis-ci.org/sanjaythakur/navigation_in_ros.svg?branch=master)](https://travis-ci.org/sanjaythakur/navigation_in_ros)

## What does this repository do?
It is a demonstration of using ROS melodic navigation stack with a custom made robot on Gazebo.

## Why make this repository?
There are a lot of resources online on the inherent codebase for automated navigation in ROS. However, they are either do not work on ROS Melodic or scattered in bits and pieces that renders them ineffective. 

Some other useful repostories are:
- https://github.com/BV-Pradeep/RIA-ROS-Navigation-in-5-days
- https://github.com/richardw05/mybot_ws
- https://github.com/rwbot/urdf_robot_creation

## What is there in this repository?
Demonstration of ROS Melodic navigation stack on
- turtlebot
- custom made robot on Gazebo 

## Some background
- What is ROS navigation stack?
- What is Gazebo?

## Instructions to use this repository?
Instructions to use navigation stack for turtlebot on ros melodic is covered first followed by the instructions for our customized robot. 
### Turtlebot3
We first go through the steps to create a map and save it. Then we will see how to use that map to enable automated navigation. 
##### Mapping
**Step 0** (optional): Open a shell and do
- ```export echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc```, and
- ```source source ~/.bashrc```

In steps 1-5, we will create a of the environment. Note that a map of an environment is a representation of the location of interest that a robot can use for navigation.

**Step 1**: Fire up the environment and a turtlebot robot by executing the following command.
- ```roslaunch turtlebot3_gazebo turtlebot3_world.launch```

**Step 2**: Launch keyboard controls.
- ```roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch```

**Step 3**: Fire up rviz.
- ```roslaunch turtlebot3_gazebo turtlebot3_gazebo_rviz.launch```
- Add *map* display to rviz and set its topic to ```\map```.

**Step 4**: Launch gmapping node.
- ```roslaunch turtlebot3_slam turtlebot3_gmapping.launch```

Drive the turtlebot around the environment a few times or until you get a decent map on rviz.

**Step 5**: Saving the map
- ```rosrun map_server map_saver -f <map_location>```

I have saved the map already under the ```map``` directory for those who want the skip the steps of creating a map.

Next we see how to leverage this map to perform automated navigation for Turtlebot.

##### Automated navigation
**Step 1**: Either keep using the same Gazebo Turtlebot environment or launch a new one using the following command.
- ```roslaunch turtlebot3_gazebo turtlebot3_world.launch```

**Step 2**: Run the following command the leverage the created map and combine the powers of ```amcl`` and ```move base```.
- ```roslaunch turtlebot3_navigation turtlebot3_navigation.launch map:=<map_location>.yaml```

**Step 3**: Set the initial pose on rviz using the ```2D Pose Estimate``` option from the menu, according to where the robot is in the Gazebo simulator.

**Step 4**: Set the intented final pose on rviz using ``2D Nav Pose``` option from the menu. You will now see the robot nicely traversing using a path that avoid obstacles.

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