link_directories(${CONAN_LIB_DIRS_GLFW} ${CONAN_LIB_DIRS_IMGUI})

add_library(gl3w STATIC GL/gl3w.c)

add_library(basic_guest SHARED basic_guest.c)
add_executable(basic_host basic_host.cpp)

add_library(basic_guest_b SHARED basic_guest_b.c)
add_executable(basic_host_b basic_host_b.cpp)

add_library(imgui_guest SHARED imgui_guest.cpp)
include_directories(.)
target_link_libraries(imgui_guest gl3w ${CONAN_LIBS_IMGUI} ${CONAN_LIBS_GLFW})

add_executable(imgui_host imgui_host.cpp)
target_link_libraries(imgui_host gl3w ${CONAN_LIBS_IMGUI} ${CONAN_LIBS_GLFW})

if(UNIX)
    target_link_libraries(basic_guest dl ${CXX_FILESYSTEM})
    target_link_libraries(basic_host dl ${CXX_FILESYSTEM})
    target_link_libraries(basic_guest_b dl ${CXX_FILESYSTEM})
    target_link_libraries(basic_host_b dl ${CXX_FILESYSTEM})

    target_link_libraries(imgui_guest dl ${CXX_FILESYSTEM})
    target_link_libraries(imgui_host dl ${CXX_FILESYSTEM})
endif()
