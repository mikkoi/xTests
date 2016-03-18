include_directories( ${STLSoft_INCLUDE_DIRS} )

add_executable( example.c.runner example.c.runner.c )
target_link_libraries( example.c.runner
  xtests.core
)
add_custom_target( examples DEPENDS example.c.runner )

