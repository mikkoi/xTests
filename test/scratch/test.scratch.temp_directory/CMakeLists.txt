include_directories (${STLSoft_INCLUDE_DIRS})

if (WIN32)
  add_executable (test.scratch.temp_directory test.scratch.temp_directory.cpp)
  target_link_libraries (test.scratch.temp_directory xtests.core)
  add_test (test.scratch.temp_directory ./test.scratch.temp_directory)
  add_custom_target(tests DEPENDS test.scratch.temp_directory)
endif (WIN32)

