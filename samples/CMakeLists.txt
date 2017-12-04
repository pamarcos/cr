add_library(basic_guest SHARED basic_guest.c)
add_executable(basic_host basic_host.cpp)

add_library(basic_guest_b SHARED basic_guest_b.c)
add_executable(basic_host_b basic_host_b.cpp)

file(GLOB GL_SRC
    "GL/*.h"
    "GL/*.cpp"
)

add_library(imgui_guest SHARED imgui_guest.cpp ${GL_SRC})
include_directories(.)
link_directories(${CONAN_LIB_DIRS_GLFW} ${CONAN_LIB_DIRS_IMGUI})
target_link_libraries(imgui_guest ${CONAN_LIBS_GLFW})

add_executable(imgui_host imgui_host.cpp ${GL_SRC})
target_link_libraries(imgui_host ${CONAN_LIBS_GLFW} ${CONAN_LIBS_IMGUI})

if (UNIX)
    target_link_libraries(basic_guest dl stdc++fs)
    target_link_libraries(basic_host dl stdc++fs)
    target_link_libraries(basic_guest_b dl stdc++fs)
    target_link_libraries(basic_host_b dl stdc++fs)

    target_link_libraries(imgui_guest dl stdc++fs)
    target_link_libraries(imgui_host dl stdc++fs)
endif()

if (MSVC)
    # vs2017 filesystem support
    set_target_properties(basic_guest PROPERTIES COMPILE_FLAGS "/std:c++latest")
    set_target_properties(basic_host  PROPERTIES COMPILE_FLAGS "/std:c++latest")
    set_target_properties(imgui_guest PROPERTIES COMPILE_FLAGS "/std:c++latest")
    set_target_properties(imgui_host  PROPERTIES COMPILE_FLAGS "/std:c++latest")
endif()
