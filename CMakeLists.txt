cmake_minimum_required(VERSION 3.8)
project(msgcom)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(ackermann_msgs REQUIRED)

# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)

add_executable(main src/main.cpp src/com_node.cpp)

ament_target_dependencies(main rclcpp std_msgs ackermann_msgs)


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

target_include_directories(main PUBLIC
$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
$<INSTALL_INTERFACE:include>)

install(TARGETS
  main
  DESTINATION lib/${PROJECT_NAME})
install(
  DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
install(
  DIRECTORY config
  DESTINATION share/${PROJECT_NAME}
)
install(TARGETS
main
DESTINATION share/${PROJECT_NAME})

ament_package()
