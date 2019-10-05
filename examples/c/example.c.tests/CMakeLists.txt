include_directories( ${STLSoft_INCLUDE_DIRS} )

add_executable(example.c.tests example.c.tests.c)
target_link_libraries(example.c.tests xTests)

