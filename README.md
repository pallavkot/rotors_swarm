# RotorS (ROS Melodic and Gazebo 9.0)
RotorS is a MAV gazebo simulator. It provides some multirotor models such as the AscTec Hummingbird, the AscTec Pelican, or the AscTec Firefly, but the simulator is not limited for the use with these multicopters.
This package also contains some example controllers, basic worlds, a joystick interface, and example launch files.

This package has some updated instructions on how to install RotorS on ROS Melodic and Gazebo 9.0 with added dependencies and packages.

The original project can be found at https://github.com/ethz-asl/rotors_simulator.
For more instructions and examples please visit the Wiki page at https://github.com/ethz-asl/rotors_simulator/wiki

## Installation Instructions - Ubuntu 18.04 and ROS Melodic
These instructions will get you a copy of the RotorS project up and running on your local machine for development and testing purposes.

### 1. Install ROS Melodic Desktop Full version on Ubuntu 18.04
```
$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
$ sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
$ sudo apt update
$ sudo apt install ros-melodic-desktop-full
$ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
$ source ~/.bashrc
$ sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
$ sudo apt install python-rosdep
$ sudo rosdep init
$ rosdep update
```
### 2. Initialize a ROS workspace
```
$ mkdir -p ~/rotors_ws/src
$ cd ~/rotors_ws/src
$ catkin_init_workspace  # initialize your catkin workspace
$ wstool init
```
### 3. Additional packages which are required for RotorS package to work
```
$ sudo apt-get install ros-melodic-joy python-catkin-tools ros-melodic-control-toolbox ros-melodic-octomap-ros ros-melodic-mavlink libgeographic-dev geographiclib-tools libgoogle-glog-dev protobuf-compiler
$ sudo apt-get update
```

### 4. Gettings the ROS install file for Rotors Package and building the workspace
```
$ wget https://raw.githubusercontent.com/ethz-asl/rotors_simulator/master/rotors_hil.rosinstall
$ wstool merge rotors_hil.rosinstall
$ wstool update
$ cd ~/rotors_ws/
$ catkin build
```
Add sourcing to your .bashrc file with 
``` 
$ source devel/setup.bash
```
### 5. Common build time errors and solutions
For error in `octomap-msgs`, install 
```
$ sudo apt-get install ros-melodic-octomap-msgs
```
For error in `future` package, install
```
$ sudo apt-get install python-pip
$ sudo pip install future
```
For error `rotors_hil_interface/hil_interface.h:105:3: error: ‘mavlink_hil_gps_t’ does not name a type mavlink_hil_gps_t hil_gps_msg_`
you need to ignore the `rotors_hil_interface`. The issue can be found at https://github.com/ethz-asl/rotors_simulator/issues/356
```
$ touch src/rotors_simulator/rotors_hil_interface/CATKIN_IGNORE
```
> Hopefully everything should be working now.

## Basic Commands
Launch the simulator with the AscTec Firefly in a basic world. 
```
$ roslaunch rotors_gazebo mav_hovering_example.launch mav_name:=firefly world_name:=basic
```
> Note: Might take some time for gazebo and models to launch. Other world files are also available in `rotors_gazebo/worlds` folder.

The simulator starts by default in paused mode. To start it you can either

 - Use the Gazebo GUI and press the play button

 - or you can send the following service call 
 ``` $ rosservice call gazebo/unpause_physics ```
 
 ## Description of other launch files
 (will be added later)
 
