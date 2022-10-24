cmake_minimum_required(VERSION 3.8)
project(interface_test)

set(CMAKE_CXX_STANDARD 17)

find_package(rosidl_generator_cpp REQUIRED)
find_package(rclcpp REQUIRED)
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(cv_bridge REQUIRED)
find_package(rosbag2_cpp REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(image_transport REQUIRED)

set(basic_interface_FOUND True)
set(advanced_interface_FOUND True)

include_directories(
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_generator_cpp/
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_typesupport_introspection_cpp/
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_generator_c/
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_typesupport_introspection_c/
	)


include_directories(
	${CMAKE_BINARY_DIR}/advanced_interface/rosidl_generator_cpp/
	${CMAKE_BINARY_DIR}/advanced_interface/rosidl_generator_c/
	${CMAKE_BINARY_DIR}/advanced_interface/rosidl_typesupport_introspection_c/
	)

add_subdirectory(advanced_interface)

add_executable(talker talker.cpp)

add_dependencies(talker basic_interface)
add_dependencies(talker advanced_interface)

target_link_libraries( talker
	basic_interface__rosidl_typesupport_cpp
	basic_interface__rosidl_typesupport_introspection_cpp
	basic_interface__rosidl_typesupport_fastrtps_cpp

	advanced_interface__rosidl_typesupport_cpp
	advanced_interface__rosidl_typesupport_introspection_cpp
	advanced_interface__rosidl_typesupport_fastrtps_cpp

	/opt/ros/galactic/lib/librclcpp.so
	/opt/ros/galactic/lib/librcutils.so
	/opt/ros/galactic/lib/librcl.so
	/opt/ros/galactic/lib/librmw.so
	/opt/ros/galactic/lib/libtracetools.so
	/opt/ros/galactic/lib/libtracetools_status.so
	/opt/ros/galactic/lib/librosidl_typesupport_c.so
	/opt/ros/galactic/lib/librosidl_typesupport_fastrtps_c.so
	/opt/ros/galactic/lib/librosidl_typesupport_fastrtps_cpp.so
	/opt/ros/galactic/lib/librosidl_typesupport_cpp.so
	/opt/ros/galactic/lib/libstd_msgs__rosidl_typesupport_cpp.so
	/opt/ros/galactic/lib/liblibstatistics_collector.so
	/opt/ros/galactic/lib/libstatistics_msgs__rosidl_typesupport_cpp.so
	)

target_include_directories(talker
	PUBLIC

	${CMAKE_BINARY_DIR}/advanced_interface/rosidl_generator_cpp/
	${CMAKE_BINARY_DIR}/advanced_interface/rosidl_generator_c/
	${CMAKE_BINARY_DIR}/advanced_interface/rosidl_typesupport_introspection_c/
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_generator_cpp/
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_generator_c/
	${CMAKE_BINARY_DIR}/advanced_interface/basic_interface/rosidl_typesupport_introspection_c/
	)

ament_export_dependencies(rosidl_default_runtime)

install(TARGETS
	talker
	DESTINATION lib/${PROJECT_NAME})

ament_package()

