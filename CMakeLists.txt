cmake_minimum_required(VERSION 3.17)

SET(COVERAGE OFF CACHE BOOL "Coverage")
SET(CMAKE_CXX_COMPILER "/usr/bin/g++")

project(Tests)

add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/third-party/gtest" "gtest")
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/banking)
add_executable(Tests ${CMAKE_CURRENT_SOURCE_DIR}/tests/test.cpp)

if (COVERAGE)
    target_compile_options(Tests PRIVATE --coverage)
    target_link_libraries(Tests PRIVATE --coverage)
endif()

target_include_directories(Tests PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/banking)
target_link_libraries(Tests PRIVATE banking gtest gtest_main gmock_main)
