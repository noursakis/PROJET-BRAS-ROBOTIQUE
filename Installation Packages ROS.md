# installation des packages ROS: 
interbotix_descriptions /interbotix_sdk / interbotix_gazebo / interbotix_moveit

Dans un terminal Ubuntu , on crée un Catkin workspace qu'on appelle interbotix_ws.
```bash
$ mkdir -p ~/interbotix_ws/src
$ cd ~/interbotix_ws/
$ catkin_make
```
on s'assure que  espace de travail est sourcé à chaque fois qu'un terminal est ouvert.
```bash
$ source ~/interbotix_ws/devel/setup.bash
$ echo "source ~/interbotix_ws/devel/setup.bash" >> ~/.bashrc
```
Dand l'espace de travail , on clone le git de interbotix_ros_arms /distribution Noetic
```bash
$ cd ~/interbotix_ws/src
$ git clone https://github.com/Interbotix/interbotix_ros_arms.git
$ cd ~/interbotix_ws/src/interbotix_ros_arms
$ git checkout noetic
```
On s'assure que toutes les dépendances requises sont installées
```bash
$ cd ~/interbotix_ws
$ rosdep update
$ rosdep install --from-paths src --ignore-src -r -y
```
On installe python3 ainsi que la bibliothéque modern_robotics 
```bash
$ sudo apt install python-pip
$ sudo pip install modern_robotics
```
une fois toutes les dépendances installés on fait un répertoire catkin:
```bash
$ cd ~/interbotix_ws
$ catkin_make
$ source ~/.bashrc
```
On s'assure que l'ordinateur va reconnaitre le module I2D2 une fois le robot connecté:
```bash
$ sudo cp ~/interbotix_ws/src/interbotix_ros_arms/interbotix_sdk/10-interbotix-udev.rules /etc/udev/rules.d
$ sudo udevadm control --reload-rules && udevadm trigger
```
Branchez le câble micro-usb (qui devrait déjà être connecté à l'U2D2) à votre ordinateur et vérifiez que le port apparaît sous le lien /dev/ttyDXL
```bash
$ cd /dev
$ ls
```
Familiarisez-vous avec le modèle de robot virtuel en le lançant dans Rviz et en jouant avec le joint_state_publisher
```bash
$ roslaunch interbotix_descriptions description.launch robot_name:=px100 jnt_pub_gui:=true
```
On peut se Familiariser également avec le bras physique du robot
```bash
$ roslaunch interbotix_sdk arm_run.launch robot_name:=px100
```
Par défaut, tous les moteurs du robot sont couplés, il sera donc très difficile de le manipuler manuellement. Pour éteindre les moteurs on fait: 
```bash
$ rosservice call /px100/torque_joints_off
```
on peut manipuler librement le bras et la pince. le modèle Rviz imite avec précision le vrai robot. Pour que le robot tienne une certaine pose, maintenez manuellement le robot dans la pose souhaitée et exécutez la commande suivante :
```bash
$ rosservice call /px100/torque_joints_on
```


