# cu-perception-manipulation-stack
Contains ros packages for perception, calibration, and arm manipulation of the Jaco arm. 

## Installation

### Dependencies:

+ ros-indigo installation
+ ubuntu 14.04
+ catkin_tools: http://catkin-tools.readthedocs.io/en/latest/installing.html

Using sudo apt-get install:
+ ros-indigo-ar-track-alvar
+ ros-indigo-moveit-core
+ ros-indigo-graph-msgs
+ ros-indigo-moveit-ros-robot-interaction
+ ros-indigo-openni2-launch
+ ros-indigo-keyboard
+ ros-indigo-moveit-ros

### Setting up a workspace and adding the packages

In your home directory:
```
mkdir -p ~/ros/jaco_ws/src
cd ros/jaco_ws/src
catkin_init_workspace
cd ..
catkin build
```
Add the following github repos in the src directory in your workspace. 
```
cd src
git clone <package>
```
packages:
+ -b indigo-devel https://github.com/davetcoleman/rviz_visual_tools.git
+ https://github.com/ros-planning/moveit_robots.git
+ -b indigo-devel https://github.com/davetcoleman/moveit_visual_tools.git
+ https://github.com/correlllab/cu-perception-manipulation-stack.git
+ https://github.com/Kinovarobotics/kinova-ros.git

Note: follow kinova-ros instructions for adding udev rules. kinova-ros may fail to build. check correct include file paths in kinova_comm.cpp: #include "kinova/KinovaTypes.h" 

restart udev so it reads the new rules:

```
sudo /etc/init.d/udev restart
```

### Compile
Use "catkin build" in your workspace one more time
```
catkin build
```

### Sourcing
Assuming you were able to compile, you will need to source your packages to be able to run them:
```
gedit ~/.bashrc
```
.bashrc lines to add:
```
source /opt/ros/indigo/setup.bash 
source ~/ros/jaco_ws/devel/setup.bash

#export HOSTNAME=011305P0009.local  # To connect to Baxter
export HOSTNAME=localhost  # Jaco, etc
export ROS_MASTER_URI=http://$HOSTNAME:11311
export ROS_IP=`hostname -I | tr -d '[[:space:]]'`
```
Either open a new terminal or source that file:
```
source ~/.bashrc
```

## Running the packages
If connecting to Jaco, run:
```
roscore
```

### launch files:
```
    roslaunch openni2_launch openni2.launch 
    roslaunch camera_calibration_tool calibration.launch
    roslaunch perception interface.launch
    roslaunch kinova_bringup kinova_robot.launch
```
### rosrun scripts:
```
    rosrun image_view image_view image:=/camera/rgb/image_raw
    rosrun keyboard keyboard
```

### for finger sensors, one of the following: 
```
    rosrun finger_sensor sensor.py
    rosrun finger_sensor sensor_visual.py
```
### Main manipulation script for jaco:
```
    rosrun pick_and_place pap_with_perception.py
```

## More instructions coming soon!

