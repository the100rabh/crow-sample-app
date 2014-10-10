cmake_minimum_required (VERSION 2.6)
project (mycrowtest)

# The version number.
set (crowtest_VERSION_MAJOR 1)
set (crowtest_VERSION_MINOR 0)
 
# configure a header file to pass some of the CMake settings
# to the source code
configure_file (
  "${PROJECT_SOURCE_DIR}/crowtestConfig.h.in"
  "${PROJECT_BINARY_DIR}/crowtestConfig.h"
  )

  
# add the binary tree to the search path for include files
# so that we will find crowtestConfig.h
include_directories("${PROJECT_BINARY_DIR}")
include_directories("/home/saurabh/code/cpp/crow/include")


set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
find_package(Tcmalloc)

if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Release")
    set(CMAKE_BUILD_TYPE "Release")
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++1y")

find_package( Boost 1.52 COMPONENTS date_time filesystem system thread REQUIRED )
include_directories( ${Boost_INCLUDE_DIR} )


add_executable(mycrowtest mycrowtest.cpp)

 target_link_libraries(mycrowtest ${Boost_LIBRARIES} )

if (Tcmalloc_FOUND)
target_link_libraries(mycrowtest ${Tcmalloc_LIBRARIES})
endif(Tcmalloc_FOUND)
