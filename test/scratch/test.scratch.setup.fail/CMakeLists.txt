include_directories (${STLSoft_INCLUDE_DIRS})

add_executable (test.scratch.setup.fail test.scratch.setup.fail.c)
target_link_libraries (test.scratch.setup.fail xtests.core)
add_test (test.scratch.setup.fail ./test.scratch.setup.fail)
SET_SOURCE_FILES_PROPERTIES( test.scratch.setup.fail.c PROPERTIES LANGUAGE CXX )

