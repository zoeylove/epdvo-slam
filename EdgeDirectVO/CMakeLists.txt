cmake_minimum_required (VERSION 3.13)
project(edge_direct_vo)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_PREFIX_PATH "/usr/local/opencv/4.0.0")
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
#set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall")
#set(CMAKE_CXX_FLAGS_DEBUG ${CMAKE_CXX_FLAGS_DEBUG})

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3 -march=native")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -march=native")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -Wall")

find_package(catkin REQUIRED COMPONENTS roscpp )

find_package(OpenCV 4 REQUIRED)
find_package(OpenCV REQUIRED)
find_package (Eigen3 3.3 REQUIRED CONFIG)
find_package(Boost REQUIRED)

#message(STATUS "Path is: ’${OpenCV_PATH}'")
message("\n=====OpenCV Library=====")
message(STATUS "[Directory]:    ${OpenCV_DIR}")
message(STATUS "[Version]:      ${OpenCV_VERSION}")
message(STATUS "[Libraries]:    ${OpenCV_LIBS}")
message(STATUS "[Include Path]: ${OpenCV_INCLUDE_DIRS}")
message( "========================\n")


catkin_package(
  INCLUDE_DIRS include
  LIBRARIES edge_direct_vo
)

include_directories(${edge_direct_vo_SOURCE_DIR}/include/edge_direct_vo
                    ${edge_direct_vo_SOURCE_DIR}/Eigen
		    ${catkin_INCLUDE_DIRS})


#file(GLOB SOURCES "include/*.h" "src/*.cpp")

add_library(${PROJECT_NAME} 
	  src/Frame.cpp
  	src/Pose.cpp
  	src/Sequence.cpp
  	src/Statistics.cpp
  	src/Trajectory.cpp
  	src/EdgeDirectVO.cpp
)

#add_executable(EdgeDirectVO ${SOURCES})

target_link_libraries (${PROJECT_NAME}   ${OpenCV_LIBS} ${catkin_LIBRARIES} ${catkin_LIB_DIRS} Eigen3::Eigen )
                                    #"-lopencv_ximgproc")         
add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS} )
