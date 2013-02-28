cmake_minimum_required(VERSION 2.8.3)
project(visp_bridge)

find_package(catkin REQUIRED COMPONENTS roscpp std_msgs geometry_msgs sensor_msgs)
find_package(VISP REQUIRED)

catkin_package(
  CATKIN_DEPENDS roscpp std_msgs geometry_msgs sensor_msgs
  DEPENDS VISP
)

add_library(${PROJECT_NAME} 
  src/conversions/3dpose.cpp
  src/conversions/image.cpp 
  src/conversions/camera.cpp 
  src/vpQuaternionVector.cpp
)

add_definitions(${VISP_DEFINITIONS})
link_directories(${VISP_LIBRARY_DIRS})

install(TARGETS ${PROJECT_NAME} 
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

## Mark cpp header files for installation
install(DIRECTORY src/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h"
   PATTERN ".svn" EXCLUDE
)
