include_directories (${STLSoft_INCLUDE_DIRS})

add_executable (test.scratch.basics2 test.scratch.basics2.cpp)
target_link_libraries (test.scratch.basics2 xtests.core)
add_test (test.scratch.basics2 ./test.scratch.basics2)
add_custom_target(tests DEPENDS test.scratch.basics2)

