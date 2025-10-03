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

mkdir -p ~/ros2_ws/src            # Make a new folder for all your ROS2 work. “ros2_ws” is just the workspace name. Inside it we make a “src” folder for source code.#
cd ~/ros2_ws                      # Go into the workspace folder so we can work there. #
ls                                # list #

cd ~/ros2_ws/src                   
os2 pkg create first_pkg --build-type ament_python    
#Ask ROS2 to create a new Python package called first_pkg. It gives you a ready-made folder structure and files so you don’t have to set them up by hand.#

gedit ~/ros2_ws/src/first_pkg/package.xml   （#  <exec_depend>rclpy</exec_depend>   #）   
#add dependenc. Tell ROS2: “my package uses rclpy,” which is the Python library that talks to ROS2. If you don’t list it, the code might fail on another computer.#

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
#create a samll node#

 gedit ~/ros2_ws/src/first_pkg/setup.py     （#    'hello = first_pkg.hello:main'   #）     
 

cd ~/ros2_ws
colcon build
source install/setup.bash
ros2 run first_pkg hello
