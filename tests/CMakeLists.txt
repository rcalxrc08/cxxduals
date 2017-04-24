

include_directories (${CMAKE_CURRENT_BINARY_DIR}/googletest/googletest/include)
include_directories (${CMAKE_CURRENT_BINARY_DIR}/googletest/googletest)
add_library (gtest "googletest/googletest/src/gtest-all.cc")
IF(UNIX)
  target_link_libraries (gtest pthread)
ELSEIF(WIN32)
  target_link_libraries (gtest)
ENDIF()

# where to find cxxduals/dual
include_directories (${CMAKE_SOURCE_DIR}/)

# test binaries
add_executable (test1 test1.cpp)
target_link_libraries (test1 gtest)

add_executable (test2 test2.cpp)
target_link_libraries (test2 gtest)

# individual tests
add_test (basic test1)
add_test (differentials test2)

# CUDA
if (CUDA_FOUND)
  cuda_add_executable (cudatest1 cudatest1.cu)
  target_link_libraries (cudatest1 gtest)
  add_test (basicCUDA cudatest1)
endif (CUDA_FOUND)

