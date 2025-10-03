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
#Make a new folder for all your ROS2 work. “ros2_ws” is just the workspace name. Inside it we make a “src” folder for source code.#

cd ~/ros2_ws                     
#Go into the workspace folder so we can work there.#

ls                               
#list#

cd ~/ros2_ws/src

ros2 pkg create first_pkg --build-type ament_python    
#Ask ROS2 to create a new Python package called first_pkg. It gives you a ready-made folder structure and files so you don’t have to set them up by hand.#

gedit ~/ros2_ws/src/first_pkg/package.xml   （#  <exec_depend>rclpy</exec_depend>   #）   
#add dependency. Tell ROS2: “my package uses rclpy,” which is the Python library that talks to ROS2. If you don’t list it, the code might fail on another computer.#

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
 #This links the word hello to the Python file. So when you type ros2 run first_pkg hello, ROS2 knows which code to run.#

cd ~/ros2_ws

colcon build    
#Build the workspace. This prepares your code and sets it up so ROS2 can find and run it.#

source install/setup.bash                   
#Tell your terminal about the new package you just built. Without this, ROS2 won’t see your package.#

ros2 run first_pkg hello                   
