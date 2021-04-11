cmake_minimum_required(VERSION 3.15)

project(hello CXX)

include(${CMAKE_CURRENT_SOURCE_DIR}/conan.cmake)

set(CMAKE_BUILD_TYPE
      RelWithDebInfo)

conan_cmake_run(
    REQUIRES
    spdlog/1.5.0
    gtest/1.8.1
    BASIC_SETUP
    CMAKE_TARGETS
    BUILD
    missing)

add_executable(hello src/main.cpp)

target_link_libraries(
    hello
    PRIVATE CONAN_PKG::spdlog)

add_executable(hello_test tests/test_hello_world.cpp)

target_link_libraries(
    hello_test
    PRIVATE CONAN_PKG::gtest)

add_custom_target(test
                  COMMAND 
                  bin/hello_test --gtest_output="xml:junit.xml"
                  WORKING_DIRECTORY ${PROJECT_BINARY_DIR})