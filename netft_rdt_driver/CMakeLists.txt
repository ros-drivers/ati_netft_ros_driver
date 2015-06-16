cmake_minimum_required(VERSION 2.8.3)
project(netft_rdt_driver)

find_package(catkin REQUIRED COMPONENTS
  cmake_modules
  diagnostic_msgs
  diagnostic_updater
  geometry_msgs
  roscpp
)

find_package(Boost REQUIRED COMPONENTS system thread program_options)
find_package(CURL REQUIRED)
find_package(TinyXML REQUIRED)


catkin_package(
  INCLUDE_DIRS include
  LIBRARIES netft_rdt_driver
  CATKIN_DEPENDS diagnostic_msgs diagnostic_updater geometry_msgs roscpp
)

include_directories(
 include ${catkin_INCLUDE_DIRS} ${TinyXML_INCLUDE_DIRS}
)

add_library(netft_rdt_driver
   src/netft_rdt_driver.cpp
)

add_executable(netft_node src/netft_node.cpp)
target_link_libraries(netft_node
  netft_rdt_driver ${catkin_LIBRARIES} ${Boost_LIBRARIES} ${CURL_LIBRARIES} ${TinyXML_LIBRARIES}
)


install(TARGETS netft_rdt_driver netft_node
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
 )
