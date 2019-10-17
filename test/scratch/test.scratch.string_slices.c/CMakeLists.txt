add_executable(test.scratch.string_slices.c test.scratch.string_slices.c.c)
target_link_libraries(test.scratch.string_slices.c xTests.core STLSoft::STLSoft)
add_test(NAME test.scratch.string_slices.c COMMAND ./test.scratch.string_slices.c)
set_source_files_properties(test.scratch.string_slices.c.c PROPERTIES LANGUAGE CXX)

