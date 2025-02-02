cmake_minimum_required(VERSION 3.0)

# set(Boost_INCLUDE_DIR /usr/local/include)
# set(Boost_LIBRARY_DIR /usr/local/lib)
# find_package(Boost COMPONENTS system filesystem REQUIRED)
# include_directories(${Boost_INCLUDE_DIR})
# link_directories(${Boost_LIBRARY_DIR})
# message(${Boost_LIBRARIES})

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set (CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()

find_package(gflags REQUIRED)

set(CMAKE_BUILD_TYPE "Release")
SET(EIGEN_INCLUDE_DIR "/usr/include/eigen3")
message("Eigen path: ${EIGEN_INCLUDE_DIR}")
include_directories(${EIGEN_INCLUDE_DIR})

file(GLOB SRC "*.cpp")
# message("cpp file list: ${SRC}")
add_executable(mesh_partition ${SRC})
# target_link_libraries( mesh_partition ${Boost_LIBRARIES} )
target_link_libraries( mesh_partition gflags)
