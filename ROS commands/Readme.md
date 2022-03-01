# Readme

In this section, we are going to explore some basic commands to manipulate the robot , as well as how to create a workspace and our first node.

## Commands to test the robot
One of the best way to get motivated while working on a project , is to see the final results to have a clear image about your objectif and how you are going to proceed.

In this section , we are going to execute some built-in commands to test and to get familiarised with the robot.

### RVIZ
We open a terminal window.
We launch the roscore , then :
```bash
roslaunch interbotix_sdk arm_run.launch robot_name:=px100 use_rviz:=true use_sim:=true
```
this command launchs **RVIZ** ( ROS visualization ), the robot is displayed in its initial position, the motors are blocked and cannot be moved them manually (servomotors blocked) .


To get information on servomotor location: arm group, joint limits ...
execute this command
```bash
rosservice call /px100/get_robot_info "cmd_type: 'group' name:'arm'"
```
To block or release motors (off/on) :
```bash
rosservice call /px100/torque_joints_on
```

To get info about the robot :
```bash
rosservice call /px100/get_robot_info 
```

rqt_graph provides a GUI plugin for visualizing the ROS computation graph. In other words , it creates a dynamic graph of what's going on in the system .
It is a good way , to check if you are getting the results you are looking for , as well as for debugging.
```bash
 rosrun rqt_graph rqt_graph
 ```
 
### Gazeebo
Gazebo is an open-source 3D robotics simulator.
To run the simulator :
```bash
roslaunch interbotix_gazebo gazebo.launch robot_name:=px100 jnt_pub_gui:=true
rosservice call /gazebo/unpause_physics #to disable the pause state
```
This command will allow you to display the robot in the gazeebo environement.
