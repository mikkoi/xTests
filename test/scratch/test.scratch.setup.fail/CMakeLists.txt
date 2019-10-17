add_executable(test.scratch.setup.fail test.scratch.setup.fail.c)
target_link_libraries(test.scratch.setup.fail xTests.core STLSoft::STLSoft)
add_test(NAME test.scratch.setup.fail COMMAND ./test.scratch.setup.fail)
set_source_files_properties(test.scratch.setup.fail.c PROPERTIES LANGUAGE CXX)

