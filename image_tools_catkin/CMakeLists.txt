cmake_minimum_required(VERSION 3.5)

project(image_tools_catkin)

if(NOT WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wextra")
endif()

find_package(catkin REQUIRED COMPONENTS rclcpp rmw_implementation_cmake sensor_msgs std_msgs)
find_package(OpenCV REQUIRED)

include_directories(include ${catkin_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})

catkin_package(
  INCLUDE_DIRS include
  #CATKIN_DEPENDS rclcpp rmw_implementation_cmake sensor_msgs std_msgs
)

add_executable(cam2image
  src/cam2image.cpp
  src/options.cpp)
target_link_libraries(cam2image ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

add_executable(showimage
  src/showimage.cpp
  src/options.cpp)
target_link_libraries(showimage ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

install(TARGETS cam2image showimage
  DESTINATION bin)
