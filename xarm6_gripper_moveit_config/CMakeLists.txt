cmake_minimum_required(VERSION 2.8.3)
project(xarm6_gripper_moveit_config)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  moveit_core
  moveit_ros_planning
  moveit_ros_planning_interface
  stomp_moveit
)

include_directories("/usr/include/eigen3")

catkin_package(
  CATKIN_DEPENDS roscpp roscpp moveit_core moveit_ros_planning moveit_ros_planning_interface stomp_moveit
)

install(DIRECTORY launch DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  PATTERN "setup_assistant.launch" EXCLUDE)
install(DIRECTORY config DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(stomp_origin src/stomp_origin.cpp)
target_link_libraries(stomp_origin ${catkin_LIBRARIES} ${Boost_LIBRARIES})
install(TARGETS stomp_origin DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

add_executable(stomp_req src/stomp_req.cpp)
target_link_libraries(stomp_req ${catkin_LIBRARIES} ${Boost_LIBRARIES})
install(TARGETS stomp_req DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
