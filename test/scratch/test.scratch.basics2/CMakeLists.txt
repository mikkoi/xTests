include_directories (${STLSoft_INCLUDE_DIRS})

add_executable (test.scratch.basics2 test.scratch.basics2.cpp)
target_link_libraries (test.scratch.basics2 xTests)
add_test (test.scratch.basics2 ./test.scratch.basics2)

