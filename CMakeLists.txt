################################################################################
# Set minimum required version of cmake, project name and compile options
################################################################################
cmake_minimum_required(VERSION 3.5)
project(multibot_ros2_interface)

# Default to C++20
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 20)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

################################################################################
# Find dependencies
################################################################################
find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED) 

################################################################################
# Declare ROS messages, services and actions
################################################################################
set(msg_files
  "msg/DriverStatusStamped.msg"
  "msg/LocalTraj.msg"
  "msg/RobotConfig.msg"
  "msg/RobotState.msg"
)

set(srv_files
  "srv/Connection.srv"
  "srv/Disconnection.srv"
  "srv/DriverCommand.srv"
  "srv/ModeSelection.srv"
  "srv/Traj.srv"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  DEPENDENCIES std_msgs geometry_msgs
)

################################################################################
# Macro for ament package
################################################################################
ament_export_dependencies(rosidl_default_runtime)
ament_package()