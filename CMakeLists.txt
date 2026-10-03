# Keep the minimum version low enough for standard CI images while still supporting
# the CUDA toolkit and CPM package management used by this demo.
cmake_minimum_required(VERSION 3.18)

project(NVBenchDemo LANGUAGES CUDA CXX)

if(NOT DEFINED CMAKE_CUDA_ARCHITECTURES)
  set(CMAKE_CUDA_ARCHITECTURES native)
endif()

# Use CPM to fetch NVBench's main branch.
# CPM: https://github.com/cpm-cmake/CPM.cmake
# NVBench: https://github.com/NVIDIA/nvbench
include(cmake/CPM.cmake)
CPMAddPackage("gh:NVIDIA/nvbench#main")

add_executable(example_bench example_bench.cu)
target_link_libraries(example_bench PRIVATE nvbench::main)
