cmake_minimum_required(VERSION 3.5)
project(dev_opencv)

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
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(cv_bridge REQUIRED)
find_package(image_transport REQUIRED)
find_package(OpenCV REQUIRED)

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

add_executable(camera_vision src/camera_vision.cpp)
ament_target_dependencies(camera_vision rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)

add_executable(subscriber_camera_vision src/subscriber_camera_vision.cpp)
ament_target_dependencies(subscriber_camera_vision rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)

add_executable(pub_cam src/pub_cam.cpp)
ament_target_dependencies(pub_cam rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)

add_executable(sub_cam src/sub_cam.cpp)
ament_target_dependencies(sub_cam rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)


install(TARGETS
   camera_vision
   subscriber_camera_vision
   pub_cam
   sub_cam
   DESTINATION lib/${PROJECT_NAME}
 )

ament_package()
