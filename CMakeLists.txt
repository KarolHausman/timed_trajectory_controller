cmake_minimum_required(VERSION 2.8.3)
project(timed_trajectory_controller)

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS cmake_modules pr2_controllers_msgs pr2_controller_interface pr2_mechanism_model roscpp control_toolbox control_msgs filters realtime_tools pluginlib)


include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})
add_library(${PROJECT_NAME} src/timed_trajectory_controller.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

# Declare catkin package
catkin_package(
  CATKIN_DEPENDS cmake_modules pr2_controllers_msgs pr2_controller_interface pr2_mechanism_model roscpp control_toolbox control_msgs filters realtime_tools pluginlib
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  )

install(TARGETS timed_trajectory_controller
   RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})

install(DIRECTORY include/${PROJECT_NAME}/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})

install(FILES controller_plugins.xml
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
