cmake_minimum_required(VERSION 2.6)

project(sparse_octree)

set(VTK_DIR /Users/dillon/Downloads/VTK-build/)

find_package(VTK REQUIRED)
include(${VTK_USE_FILE})

SET(EXTRA_CXX_COMPILE_FLAGS "-std=c++11 -I./src -I./test -I/opt/local/include -O2 -Werror -Wall")

SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} ${EXTRA_CXX_COMPILE_FLAGS}")

INCLUDE_DIRECTORIES(./src/)

SET(CPP_FILES ./src/vtk_debug.cpp
	      ./src/sparse_octree.cpp
	      ./src/cylinder.cpp
	      ./src/volume_removal.cpp
	      ./src/sphere.cpp
	      ./src/vec_3.cpp)

SET(TEST_FILES ./test/sparse_octree_tests.cpp
	       ./test/volume_containment_tests.cpp
	       ./test/cylinder_tests.cpp)

add_executable(all-tests ${TEST_FILES} ${CPP_FILES})
#target_link_libraries(all-tests )

######### VTK Example ##########

# Make command:
# /opt/local/bin/cmake -DVTK_DIR:PATH=/Users/dillon/Downloads/VTK-build/ -DCMAKE_BUILD_TYPE=Debug . 

if(VTK_LIBRARIES)
  target_link_libraries(all-tests ${VTK_LIBRARIES})
else()
  target_link_libraries(all-tests vtkHybrid vtkWidgets)
endif()
