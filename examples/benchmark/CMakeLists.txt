cmake_minimum_required(VERSION 3.14 FATAL_ERROR)

project(CPMExampleBenchmark)

# ---- Dependencies ----

include(../../cmake/CPM.cmake)

CPMAddPackage(
  NAME fibonacci
  GIT_REPOSITORY https://github.com/TheLartians/Fibonacci.git
  VERSION 2.0
)

CPMAddPackage(
  NAME benchmark
  GITHUB_REPOSITORY google/benchmark
  VERSION 1.5.0
  OPTIONS
    "BENCHMARK_ENABLE_TESTING Off"
)

if (benchmark_ADDED)
  # patch google benchmark target
  set_target_properties(benchmark PROPERTIES CXX_STANDARD 17)
endif()

# ---- Executable ----

add_executable(CPMExampleBenchmark "main.cpp")
set_target_properties(CPMExampleBenchmark PROPERTIES CXX_STANDARD 17)        
target_link_libraries(CPMExampleBenchmark fibonacci benchmark)
