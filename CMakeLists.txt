project(cr)
cmake_minimum_required(VERSION 3.0.2)
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

include(conanbuildinfo.cmake)
conan_basic_setup()

enable_testing()

option(BUILD_TESTS "BUILD_TESTS" ON)
option(BUILD_SAMPLES "BUILD_SAMPLES" ON)

add_definitions("-std=c++1z")
add_definitions(-DCR_DEPLOY_PATH="${CMAKE_LIBRARY_OUTPUT_DIRECTORY}")

if (BUILD_TESTS)
    add_subdirectory(tests)
endif()

if (BUILD_SAMPLES)
    add_subdirectory(samples)
endif()

# Ensure /MT is used in MSVC
if (MSVC)
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_DEBUG ${CMAKE_CXX_FLAGS_DEBUG})
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_RELEASE ${CMAKE_CXX_FLAGS_RELEASE})
endif()
