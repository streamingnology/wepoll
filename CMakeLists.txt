cmake_minimum_required(VERSION 3.14)
project(wepoll)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

message(STATUS "operation system is ${CMAKE_SYSTEM}")
if (NOT CMAKE_SYSTEM_NAME MATCHES "Windows")
  message(FATAL_ERROR "this library is for windows only")
endif()

if( NOT CMAKE_BUILD_TYPE )
   set( CMAKE_BUILD_TYPE debug ... FORCE )
endif()

set(BUILD_MODE_DIR ".")

if (CMAKE_SYSTEM_NAME MATCHES "Windows")
  if(CMAKE_BUILD_TYPE MATCHES debug)
    message("Debug build.")
    set(BUILD_MODE_DIR "Debug")
  elseif(CMAKE_BUILD_TYPE MATCHES release)
    message("Release build.")
    set(BUILD_MODE_DIR "Release")
  else()
    message(FATAL_ERROR  "Unkown Build Type, It should be either debug or release")
  endif()
endif()

aux_source_directory(${CMAKE_CURRENT_SOURCE_DIR} WEPOLL_SOURCES)

add_library(wepoll STATIC ${WEPOLL_SOURCES})