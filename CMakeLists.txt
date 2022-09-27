cmake_minimum_required(VERSION 2.8.3)
project(sicktoolbox)

find_package(catkin REQUIRED)

## System dependencies are found with CMake's conventions
find_package(Threads REQUIRED)

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES SickLMS2xx
  CATKIN_DEPENDS
  DEPENDS Threads
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(include ${catkin_INCLUDE_DIRS})

# Driver libraries



add_library(SickLMS2xx c++/drivers/lms2xx/sicklms2xx/SickLMS2xx.cc c++/drivers/lms2xx/sicklms2xx/SickLMS2xxBufferMonitor.cc c++/drivers/lms2xx/sicklms2xx/SickLMS2xxMessage.cc)
target_link_libraries(SickLMS2xx ${catkin_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})

# Examples


add_executable(lms2xx_config c++/examples/lms2xx/lms2xx_config/src/main.cc)
target_link_libraries(lms2xx_config SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_mean_values c++/examples/lms2xx/lms2xx_mean_values/src/main.cc)
target_link_libraries(lms2xx_mean_values SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_partial_scan c++/examples/lms2xx/lms2xx_partial_scan/src/main.cc)
target_link_libraries(lms2xx_partial_scan SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_real_time_indices c++/examples/lms2xx/lms2xx_real_time_indices/src/main.cc)
target_link_libraries(lms2xx_real_time_indices SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_set_variant c++/examples/lms2xx/lms2xx_set_variant/src/main.cc)
target_link_libraries(lms2xx_set_variant SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_simple_app c++/examples/lms2xx/lms2xx_simple_app/src/main.cc)
target_link_libraries(lms2xx_simple_app SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_stream_range_and_reflect c++/examples/lms2xx/lms2xx_stream_range_and_reflect/src/main.cc)
target_link_libraries(lms2xx_stream_range_and_reflect SickLMS2xx ${catkin_LIBRARIES})

add_executable(lms2xx_subrange c++/examples/lms2xx/lms2xx_subrange/src/main.cc)
target_link_libraries(lms2xx_subrange SickLMS2xx ${catkin_LIBRARIES})

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/groovy/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
install(TARGETS SickLMS2xx
  lms2xx_config lms2xx_mean_values lms2xx_partial_scan lms2xx_real_time_indices 
  lms2xx_set_variant lms2xx_simple_app lms2xx_stream_range_and_reflect lms2xx_subrange
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

## TODO Move headers that aren't needed externally back into the source
## Mark cpp header files for installation
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hh"
  PATTERN ".svn" EXCLUDE
)

## TODO There are readmes, etc, create install rules for these
## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )
