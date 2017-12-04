project(cr)
cmake_minimum_required(VERSION 3.0.2)
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

include(conanbuildinfo.cmake)
conan_basic_setup()

enable_testing()

add_definitions("-std=c++1z")
add_definitions(-DCR_DEPLOY_PATH="${CMAKE_LIBRARY_OUTPUT_DIRECTORY}")

add_subdirectory(samples)
add_subdirectory(tests)
