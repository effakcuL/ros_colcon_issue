cmake_minimum_required(VERSION 3.8)
project(advanced_interface)

find_package(rosidl_generator_cpp REQUIRED)
find_package(rclcpp REQUIRED)
find_package(basic_interface REQUIRED)                        
find_package(ament_cmake REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
	msg/AdvancedArea.msg
	#MARKER_END_OF_MESSAGELIST
	DEPENDENCIES
	basic_interface

	)

ament_package()

