project(cr)
cmake_minimum_required(VERSION 3.0.2)
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

include(conanbuildinfo.cmake)
conan_basic_setup()

enable_testing()

option(BUILD_TESTS "BUILD_TESTS" ON)
option(BUILD_SAMPLES "BUILD_SAMPLES" ON)

add_definitions(-DCR_DEPLOY_PATH="${CMAKE_LIBRARY_OUTPUT_DIRECTORY}")

# Ensure /MT is used in MSVC
if(MSVC)
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_DEBUG ${CMAKE_CXX_FLAGS_DEBUG})
    string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_RELEASE ${CMAKE_CXX_FLAGS_RELEASE})
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++latest")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++1z")
endif()

if(APPLE)
    link_directories(/usr/local/Cellar/llvm@4/4.0.1/lib/)
    set(CXX_FILESYSTEM c++experimental)
elseif(UNIX AND NOT APPLE)
    set(CXX_FILESYSTEM stdc++fs)
    set(LINUX TRUE)
endif()

if(BUILD_TESTS)
    add_subdirectory(tests)
endif()

if(BUILD_SAMPLES)
    add_subdirectory(samples)
endif()
