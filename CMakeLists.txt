cmake_minimum_required(VERSION 2.8)

project(voro)

find_package(catkin)
find_package(Boost REQUIRED COMPONENTS filesystem system)


if(catkin_FOUND)
  catkin_package(
    INCLUDE_DIRS src/
    LIBRARIES voro
)
endif()

include_directories(${catkin_INCLUDE_DIRS} src/)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(CMAKE_CXX_FLAGS "-std=c++11 -g2 -DDEBUG ${CMAKE_CXX_FLAGS}")
else()
  set(CMAKE_CXX_FLAGS "-std=c++11 -Wall -O3 -DNDEBUG ${CMAKE_CXX_FLAGS}")
endif()

message("Using CMAKE_CXX_FLAGS = ${CMAKE_CXX_FLAGS}")


# library
add_library(voro 
	src/voro/config.hh
	src/voro/common.hh
	src/voro/common.cc
	src/voro/cell.hh
	src/voro/cell.cc
	src/voro/unitcell.hh
	src/voro/unitcell.cc
	src/voro/pre_container.hh
	src/voro/pre_container.cc
	src/voro/container_prd.hh
	src/voro/container_prd.cc
	src/voro/container.hh
	src/voro/container.cc
	src/voro/v_compute.hh
	src/voro/v_compute.cc
	src/voro/worklist.hh
	src/voro/rad_option.hh
	src/voro/c_loops.hh
	src/voro/c_loops.cc
	src/voro/v_base.hh
	src/voro/v_base.cc
	src/voro/v_base_wl.cc
	src/voro/wall.hh
	src/voro/wall.inline.hh
	src/voro/wall.cc
	src/voro/voro++.hh
	)

#add_executable(voro-console 
#	src/cmd_line.cc
#	)
	
#target_link_libraries(voro-console
#	voro
#	)

target_link_libraries(voro ${Boost_LIBRARIES})
