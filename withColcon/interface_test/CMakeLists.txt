cmake_minimum_required(VERSION 3.8)
project(interface_test)

find_package(rosidl_generator_cpp REQUIRED)
find_package(basic_interface REQUIRED)                        
find_package(advanced_interface REQUIRED)                        
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)



add_executable(talker talker.cpp)
ament_target_dependencies(talker rclcpp basic_interface advanced_interface)        
ament_export_dependencies(rosidl_default_runtime)

install(TARGETS
	talker
	DESTINATION lib/${PROJECT_NAME})

ament_package()

