# add a target to generate API documentation with Doxygen
find_package( Doxygen QUIET )
if( DOXYGEN_FOUND )
  configure_file(
      ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in
      ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile @ONLY
  )
  add_custom_target( docs
    ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    COMMENT "Generating API documentation with Doxygen" VERBATIM
  )
else( DOXYGEN_FOUND )
    message( STATUS "Doxygen not found. Unable to generate documentation." )
endif( DOXYGEN_FOUND )

