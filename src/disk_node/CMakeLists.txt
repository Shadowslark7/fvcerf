cmake_minimum_required(VERSION 3.0.2)
project(disk_node)

set(SOURCE_FILES
        communicator.h
        communicator.cpp
        )

add_library(disk_node STATIC ${SOURCE_FILES})
