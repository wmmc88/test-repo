cmake_minimum_required(VERSION 3.14.4)
project(test_pkg)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

add_executable(test_node src/main.cpp)
ament_target_dependencies(test_node
    "rclcpp")


if (BUILD_TESTING)
  # generate compile_commands.json for clang-tidy
  set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE INTERNAL "")

  # cppcheck
  find_package(ament_cmake_cppcheck REQUIRED)
  ament_cppcheck()

  # clang-format
  find_package(ament_cmake_clang_format REQUIRED)
  ament_clang_format()

  # clang-tidy
  find_package(ament_cmake_clang_tidy REQUIRED)
  ament_clang_tidy(${CMAKE_BINARY_DIR})

  # flake8
  find_package(ament_cmake_flake8 REQUIRED)
  ament_flake8()

  # xmllint
  find_package(ament_cmake_xmllint REQUIRED)
  ament_xmllint()
endif ()

ament_package()
