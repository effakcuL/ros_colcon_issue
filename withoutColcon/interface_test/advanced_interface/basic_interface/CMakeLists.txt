cmake_minimum_required(VERSION 3.8)
project(basic_interface)


if (CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
	add_compile_options(-Wall -Wextra -Wpedantic)
endif ()



find_package(rosidl_default_generators REQUIRED)
find_package(ament_cmake REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
	"msg/Feature/Area.msg"
	"msg/Feature/Circle.msg"
	"msg/Feature/Feature.msg"
	"msg/Feature/Line.msg"
	"msg/Feature/MovingPoint.msg"
	"msg/Feature/Point.msg"
	"msg/Types/Position.msg"
	"msg/Types/Velocity.msg"
	"msg/Types/Rotation.msg"
	)

ament_package()

