cmake_minimum_required(VERSION 3.15)

project(hello CXX)

include(${CMAKE_CURRENT_SOURCE_DIR}/conan.cmake)

set(CMAKE_BUILD_TYPE
      RelWithDebInfo)

conan_cmake_run(
    REQUIRES
    spdlog/1.5.0
    BASIC_SETUP
    CMAKE_TARGETS
    BUILD
    missing)

add_executable(hello src/main.cpp)

target_link_libraries(
    hello
    PRIVATE CONAN_PKG::spdlog)