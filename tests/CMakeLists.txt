add_library(test_basic SHARED test_basic.cpp test_data.h test_basic.x)
add_executable(crTest test.cpp test_data.h test_basic.x)

link_directories(${CONAN_LIB_DIRS_GTEST})
target_link_libraries(crTest ${CONAN_LIBS_GTEST})

if (UNIX)
    target_link_libraries(crTest dl stdc++fs)
    set_target_properties(crTest PROPERTIES COMPILE_FLAGS "-fno-stack-protector")
endif()

add_test(crTest ${CMAKE_BINARY_DIR}/bin/crTest)
