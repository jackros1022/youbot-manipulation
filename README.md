## youbot_manipulation

This repository contains packages for using the youBot's manipulator in ROS. It includes an analytical inverse position kinematics solver and configuration files for MoveIt!.


### Overview
The youbot_manipulation meta-package contains the following packages:
* youbot_arm_kinematics: A framework-independent library which implements an analytical inverse position kinematics solver for the youBot manipulator.
* youbot_arm_kinematics_moveit: A MoveIt! plugin which exposes the youbot_arm_kinematics library (see above) to MoveIt!.
* youbot_moveit: Configuration files to use the youBot with MoveIt! and the analytical inverse kinematics solver from this repository. These files have been auto-generated by the MoveIt! setup assistant.


### Prerequisites
First, install the required ROS and especially MoveIt! packages by executing:

    apt-get install python-wstool ros-hydro-roscpp ros-hydro-pluginlib ros-hydro-urdf \
      ros-hydro-tf-conversions ros-hydro-joint-state-publisher \
      ros-hydro-robot-state-publisher ros-hydro-xacro \
      ros-hydro-moveit-core ros-hydro-moveit-ros-move-group \
      ros-hydro-moveit-planners-ompl ros-hydro-moveit-ros-visualization

Then, create a Catkin workspace (http://wiki.ros.org/catkin/Tutorials/create_a_workspace) and add the youBot description repository with the following commands:

    cd <catkin_workspace>/src
    wstool init
    wstool set youbot_description --git git@github.com:youbot/youbot_description.git --version=hydro-devel
    wstool update youbot_description

### Installation
Add the youBot manipulation repository to this workspace by executing the following commands:

    cd <catkin_workspace>/src
    wstool set youbot_manipulation --git git@github.com:svenschneider/youbot-manipulation.git --version=hydro
    wstool update youbot_manipulation

Now build the workspace:

    cd <catkin_workspace>
    catkin_make


### Running the demo
The youbot_moveit package contains a demo to run and visualize a simulated youBot in RViz. This demo can be executed via the following command:

    roslaunch youbot_moveit demo.launch

Using the markers attached to the manipulator, the end-effector can be dragged around which triggers the inverse kinematics solver. Additionally, different motion planners can be tried out.


### Running on the real or simulated robot
First, bring up the real or simulated robot. Then, start MoveIt! via:

    roslaunch youbot_moveit move_group.launch

With the MoveIt! Commander (http://moveit.ros.org/wiki/MoveIt_Commander) the manipulator can be moved by typing in commands. To start the MoveIt! Commander run:

    rosrun moveit_commander moveit_commander_cmdline.py

Then select the hardware group to move and command it to some known position (e.g. the up-right, candle position):

    > use arm_1
    arm_1> go candle


### Documentation

The MoveIt! kinematics plugin in the youbot_arm_kinematics_moveit package implements the standard MoveIt! interfaces. Therefore, consult the MoveIt! website (http://moveit.ros.org/) for further documentation related to using MoveIt!.
