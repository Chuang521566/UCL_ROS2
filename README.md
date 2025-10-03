wget http://fishros.com/install -O fishros && . fishros

ros2 run turtlesim turtlesim_node

ros2 run turtlesim turtle_teleop_key

ros2 topic echo /turtle1/pose

rqt

sudo apt update
sudo apt install ros-foxy-gazebo-ros-pkgs
gazebo
rviz2
