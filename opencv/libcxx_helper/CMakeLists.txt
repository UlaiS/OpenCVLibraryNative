cmake_minimum_required(VERSION 3.6)

set(target detection_based_tracker)
project(${target} CXX)

set(ANDROID_OPENCV_COMPONENTS "opencv_java" CACHE STRING "")
message(STATUS "ANDROID_ABI=${ANDROID_ABI}")
find_package(OpenCV REQUIRED COMPONENTS ${ANDROID_OPENCV_COMPONENTS})

file(GLOB srcs *.cpp *.c)
file(GLOB hdrs *.hpp *.h)

message(STATUS "OpenCV libraries: ${OpenCV_LIBS}")

include_directories(${OpenCV_INCLUDE_DIRS})
include_directories("${CMAKE_CURRENT_LIST_DIR}")
add_library(${target} SHARED ${srcs} ${hdrs})

#target_link_libraries (${target} jnigraphics)
target_link_libraries(${target} ${ANDROID_OPENCV_COMPONENTS} ${OpenCV_LIBS})