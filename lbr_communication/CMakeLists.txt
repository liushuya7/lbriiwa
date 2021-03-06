cmake_minimum_required(VERSION 3.5)
project(lbr_communication)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclpy REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(lbr_msgs REQUIRED)

# Install the python module for this package
ament_python_install_package(script/)
ament_python_install_package(nodes/)


################################################################################
# Declare ROS messages, services and actions
################################################################################


#add_executable(dummy_joint_states dummy_joint_states.cpp)
#ament_target_dependencies(dummy_joint_states "rclcpp" "sensor_msgs")


# Install C++ headers
#install(
#  DIRECTORY include/${PROJECT_NAME}/
#  DESTINATION include/${PROJECT_NAME}
#  FILES_MATCHING PATTERN "*.hpp"
#)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()


# Install python scripts
install(
  DIRECTORY launch param script
  DESTINATION share/${PROJECT_NAME}
)

install(
  PROGRAMS
    script/view_frames.py
    script/buffer.py
    script/tcpSocket.py
    script/udpSocket.py
    nodes/lbr_statusdata_node.py
    nodes/lbr_sensordata_node.py
    nodes/lbr_commands_node.py
    DESTINATION lib/${PROJECT_NAME}
)

ament_package()
