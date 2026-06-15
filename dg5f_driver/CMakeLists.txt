cmake_minimum_required(VERSION 3.12)
project(dg5f_driver)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# 1. 필수 의존성 패키지 검색
find_package(ament_cmake REQUIRED)

# 💡 [Lyrical 핵심 패치] 분가한 타겟 종속성 패키지를 명시적으로 로드합니다!
find_package(ament_cmake_target_dependencies REQUIRED) 

find_package(rclcpp REQUIRED)
find_package(hardware_interface REQUIRED)
find_package(delto_hardware REQUIRED)
find_package(delto_tcp_comm REQUIRED)

# 2. 파이썬 스크립트 및 실행 파일 인스톨 설정
install(
  PROGRAMS
  script/dg5f_left_pid_test.py
  script/dg5f_right_pid_test.py
  script/dg5f_left_pid_all_test.py
  script/dg5f_right_pid_all_test.py
  script/manus_retarget/manus_retarget.py
  DESTINATION lib/${PROJECT_NAME}
)

# 3. 헤더 디렉토리 인스톨 설정
install(
  DIRECTORY include/
  DESTINATION include
)

# 4. 로봇 설정, URDF 모델, 런치 파일 인스톨 설정
install(
  DIRECTORY config urdf launch
  DESTINATION share/${PROJECT_NAME}
)

# 5. 테스트 빌드 린트 설정
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

# 6. 패키지 마감 매크로
ament_package()
