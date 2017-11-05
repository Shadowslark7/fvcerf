cmake_minimum_required(VERSION 3.0.2)
project(tests)

# Download and unpack googletest at configure time
configure_file(CMakeLists.txt.in googletest-download/CMakeLists.txt)
execute_process(COMMAND "${CMAKE_COMMAND}" -G "${CMAKE_GENERATOR}" .
        WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/src/tests/googletest-download" )
execute_process(COMMAND "${CMAKE_COMMAND}" --build .
        WORKING_DIRECTORY "${CMAKE_BINARY_DIR}/src/tests/googletest-download" )

# Prevent GoogleTest from overriding our compiler/linker options
# when building with Visual Studio
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Add googletest directly to our build. This adds
# the following targets: gtest, gtest_main, gmock
# and gmock_main
add_subdirectory("${CMAKE_BINARY_DIR}/googletest-src"
        "${CMAKE_BINARY_DIR}/googletest-build")


include_directories("${gtest_SOURCE_DIR}/include"
        "${gmock_SOURCE_DIR}/include")

file(GLOB TEST_SRC_FILES *.cpp)

add_executable(tests ${TEST_SRC_FILES})
target_link_libraries(tests gtest gmock_main)

add_custom_command(TARGET tests POST_BUILD COMMAND tests)

