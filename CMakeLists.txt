
#
# CMake for cxxduals
#
cmake_minimum_required (VERSION 2.6.8)

# Default build mode
if (NOT CMAKE_BUILD_TYPE)
  set (CMAKE_BUILD_TYPE "RelWithDebInfo")
endif (NOT CMAKE_BUILD_TYPE)

#
# Project Name
#
project (cxxduals CXX)
IF(WIN32)
  set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
ELSEIF(UNIX)
  set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -std=c++11")
ENDIF()
include_directories(cxxduals)
find_package (CUDA)
if (CUDA_FOUND)
  set (CUDA_HOST_COMPILER ${CMAKE_CXX_COMPILER})
  set (CUDA_PROPAGATE_HOST_FLAGS OFF)
  set (CUDA_NVCC_FLAGS "${CUDA_NVCC_FLAGS} -std=c++11; --compiler-options -Wall -g")

  #LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_20,code=sm_20)
  LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_30,code=sm_30)
  #LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_35,code=sm_35)
  #LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_37,code=sm_37)
  #LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_50,code=sm_50)
  #LIST(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_52,code=sm_52)

endif (CUDA_FOUND)

enable_testing ()

add_subdirectory (tests)
add_subdirectory (examples)
