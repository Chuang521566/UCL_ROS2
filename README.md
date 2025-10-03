# One Line Insatallation Code #
wget http://fishros.com/install -O fishros && . fishros

# Output ROS Version #
source /opt/ros/foxy/setup.bash
echo $ROS_DISTRO  

# Turtle Node Example #

ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key
ros2 topic echo /turtle1/pose
rqt

# Try Gazebo and Rviz #

sudo apt update
sudo apt install ros-foxy-gazebo-ros-pkgs
gazebo
rviz2


# First Package Example #

mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
ls

cd ~/ros2_ws/src
os2 pkg create first_pkg --build-type ament_python
gedit ~/ros2_ws/src/first_pkg/package.xml   （#  <exec_depend>rclpy</exec_depend>   #）

gedit ~/ros2_ws/src/first_pkg/first_pkg/hello.py     
(#   import rclpy
from rclpy.node import Node

def main():
    rclpy.init()
    node = Node('hello_node')                 # Create Node
    node.get_logger().info('Hello from ROS 2 Foxy!')
    node.destroy_node()                       # Clean up
    rclpy.shutdown()
 #)

 gedit ~/ros2_ws/src/first_pkg/setup.py     （#    'hello = first_pkg.hello:main'   #）

cd ~/ros2_ws
colcon build
source install/setup.bash
ros2 run first_pkg hello
