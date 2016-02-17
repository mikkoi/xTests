include_directories (${STLSoft_INCLUDE_DIRS})

add_executable (test.scratch.basics1 test.scratch.basics1.c)
target_link_libraries (test.scratch.basics1 xtests.core)
add_test (test.scratch.basics1 ./test.scratch.basics1)
SET_SOURCE_FILES_PROPERTIES( test.scratch.basics1.c PROPERTIES LANGUAGE CXX )
add_custom_target(tests DEPENDS test.scratch.basics1)

