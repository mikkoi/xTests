include_directories (${STLSoft_INCLUDE_DIRS})

add_executable (test.scratch.fail_all.1 test.scratch.fail_all.1.cpp)
target_link_libraries (test.scratch.fail_all.1 xtests.core)
add_test (test.scratch.fail_all.1 ./test.scratch.fail_all.1)

