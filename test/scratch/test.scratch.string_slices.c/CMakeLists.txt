include_directories (${STLSoft_INCLUDE_DIRS})

add_executable (test.scratch.string_slices.c test.scratch.string_slices.c.c)
target_link_libraries (test.scratch.string_slices.c xtests.core)
add_test (test.scratch.string_slices.c ./test.scratch.string_slices.c)
SET_SOURCE_FILES_PROPERTIES( test.scratch.string_slices.c.c PROPERTIES LANGUAGE CXX )

