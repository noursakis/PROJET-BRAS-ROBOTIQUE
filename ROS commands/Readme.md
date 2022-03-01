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

## Record/Play

In this section , we are going to execute a more complicated and interesting command.

First , we will record a random mouvement by moving our robot in different directions.
To do so :
```bash
roslaunch interbotix_puppet_control puppet_control_single.launch robot_name:=px100
```
It's recommended that the mouvement should not be too fast , to make the recording more efficient.
After finishing the recording , we type Ctrl+C to kill the command.

To playback the motion, type the following in the terminal:
```bash
roslaunch interbotix_xsarm_puppet xsarm_puppet_single.launch robot_model:=px100 playback:=true
```
The robot should now repeat the motions.
To visualize the motion on RVIZ , you need to play the correspending bag file in the bag directory *(interbotix_ros_manipulators/interbotix_ros_xsarms/examples/interbotix_xsarm_puppet/bag/)* : 
```bash
rosbag play px100_commands.bag
```

## Creating Workspace/Package/Node

### Workspace
After making sure that our robot is recognized by our ROS system , now we are going to create our own workspace and our our own nodes ( programs ).

To create a workspace :
```bash
mkdir -p ~/catkin_ws/src
cd ..
```
After creating a workspace , we compile and source :
```bash
catkin_make
source devel/setup.bash # sourcing the workspace 
```

### Package
While inside the workspace folder :
```bash
cd src
catking_create_pkg test std_msgs rospy roscpp 
```
This command creates a package ( folder ) named test , with std_msgs , rospy , roscpp as dependencies. For more info, click [here](http://wiki.ros.org/ROS/Tutorials/CreatingPackage) .

### Node : Publisher/Subscriber

We choosed to write our programms using python.
For this step , it's recommended to visit the official website to get a better understanding about the Publisher/Subscriber node.[Here_1](http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29) then [Here_2](http://wiki.ros.org/ROS/Tutorials/ExaminingPublisherSubscriber).

Once finishe writting the program , make it executable and build it:
```bash
chmod +x publisher.py # it will become green
catkin_make # in the workspace folder
```
To run the program : 

```bash
rosrun test publisher.py
```

