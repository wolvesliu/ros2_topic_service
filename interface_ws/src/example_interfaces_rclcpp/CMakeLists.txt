cmake_minimum_required(VERSION 3.8)
project(example_interfaces_rclcpp)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(example_ros2_interfaces REQUIRED)



if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()


#新增：生成可执行文件example_interfaces_control_01_node 节点到名称
add_executable(example_interfaces_control_01_node src/example_interfaces_control_01_node.cpp)
add_executable(example_interfaces_robot_01_node   src/example_interfaces_robot_01_node.cpp)

target_include_directories(example_interfaces_control_01_node PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)
target_compile_features(example_interfaces_control_01_node PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17


target_include_directories(example_interfaces_robot_01_node PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)
target_compile_features(example_interfaces_robot_01_node PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17


ament_target_dependencies(example_interfaces_control_01_node 
  rclcpp 
  example_ros2_interfaces)

ament_target_dependencies(example_interfaces_robot_01_node 
  rclcpp 
  example_ros2_interfaces)

install(TARGETS
example_interfaces_control_01_node
  DESTINATION lib/${PROJECT_NAME}
)

install(TARGETS
example_interfaces_robot_01_node
  DESTINATION lib/${PROJECT_NAME}
)