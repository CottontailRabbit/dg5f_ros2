cmake_minimum_required(VERSION 3.12)
project(dg5f_driver)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_target_dependencies REQUIRED) 
find_package(rclcpp REQUIRED)
find_package(hardware_interface REQUIRED)
find_package(delto_hardware REQUIRED)
find_package(delto_tcp_comm REQUIRED)

# Install
install(
  PROGRAMS
  script/dg5f_left_jtc_test.py
  script/dg5f_right_jtc_test.py
  script/dg5f_left_pid_test.py
  script/dg5f_right_pid_test.py
  script/dg5f_left_pid_all_test.py
  script/dg5f_right_pid_all_test.py
  script/manus_retarget/manus_retarget.py
  DESTINATION lib/${PROJECT_NAME}
)

install(
  DIRECTORY include/
  DESTINATION include
)

install(
  DIRECTORY config urdf launch
  DESTINATION share/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
