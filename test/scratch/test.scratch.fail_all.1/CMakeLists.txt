add_executable(test.scratch.fail_all.1 test.scratch.fail_all.1.cpp)
target_link_libraries(test.scratch.fail_all.1 xTests.core STLSoft::STLSoft)
add_test(NAME test.scratch.fail_all.1 COMMAND ./test.scratch.fail_all.1)

