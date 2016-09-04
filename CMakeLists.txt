cmake_minimum_required(VERSION 2.8.12)

# In-source build prevention.
if(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})
  message(STATUS "Project requires an out-of-source build.")
  message(STATUS "Please remove these files from ${CMAKE_BINARY_DIR} first:")
  message(STATUS "CMakeCache.txt")
  message(STATUS "CMakeFiles")
  message(STATUS "Once these files are removed, create a separate directory")
  message(STATUS "and run CMake from there.")
  message(FATAL_ERROR "in-source build detected")
endif()

project(CUDD)

####################### Begin Options ###################

# option(CUDD_BUILD_TESTS "Build the tests" ON)

####################### End Options ###################

####################### Begin compiler configurations ###################

option(PACKAGE "Package for distribution" OFF)
include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX11)
if(NOT COMPILER_SUPPORTS_CXX11)
  message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support.")
endif()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

######################## End compiler configurations ####################

##################### Begin cmake configuration ###################

# Set project directories.
set(PROJECT_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(CUDD_SOURCE_DIR "${PROJECT_SOURCE_DIR}/cudd")
set(CUDD_CPP_DIR "${PROJECT_SOURCE_DIR}/cplusplus")
set(CUDD_UTIL_DIR "${PROJECT_SOURCE_DIR}/util")
set(CUDD_EPD_DIR "${PROJECT_SOURCE_DIR}/epd")
set(CUDD_MTR_DIR "${PROJECT_SOURCE_DIR}/mtr")
set(CUDD_ST_DIR "${PROJECT_SOURCE_DIR}/st")

######################## End cmake configuration ###################

########################## Begin includes ###############################

include_directories("${PROJECT_SOURCE_DIR}")  # TODO: Remove when config.h is gone.

add_subdirectory("${CUDD_EPD_DIR}")
add_subdirectory("${CUDD_MTR_DIR}")
add_subdirectory("${CUDD_ST_DIR}")
add_subdirectory("${CUDD_UTIL_DIR}")
add_subdirectory("${CUDD_CPP_DIR}")
add_subdirectory("${CUDD_SOURCE_DIR}")

####################### End includes ####################################
