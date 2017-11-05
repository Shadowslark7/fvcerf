cmake_minimum_required(VERSION 3.0.2)
project (engine)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -march=native -Wall")

add_subdirectory(disk_node)
add_subdirectory(tests)
