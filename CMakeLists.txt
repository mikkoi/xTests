cmake_minimum_required (VERSION 2.6)
project (xTests C CXX)
enable_testing()
set(xTests_VERSION 0.18.4)

# Assuming test library will always be linked statically.
set (BUILD_SHARED_LIBS FALSE)

# Project include directory (all includes located here)
include_directories ("${CMAKE_CURRENT_SOURCE_DIR}/include")

find_package(STLSoft 1.9.125 REQUIRED)

add_subdirectory (src)

# build target 'tests' for tests.
add_subdirectory (test EXCLUDE_FROM_ALL)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_INCLUDE_CURRENT_DIR_IN_INTERFACE ON)

include(GenerateExportHeader)
include(CMakePackageConfigHelpers)

include_directories (${STLSoft_INCLUDE_DIRS})
add_library(xTests src/xtests.core.cpp)
generate_export_header(xTests)
set_property(TARGET xTests PROPERTY VERSION ${xTests_VERSION})
set_property(TARGET xTests PROPERTY INTERFACE_xTests_MAJOR_VERSION ${xTests_VERSION})
set_property(TARGET xTests APPEND PROPERTY
  COMPATIBLE_INTERFACE_STRING xTests_MAJOR_VERSION
)

install( TARGETS xTests EXPORT xTestsTargets
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
)
install( DIRECTORY
    "${CMAKE_CURRENT_SOURCE_DIR}/include/xtests"
  DESTINATION include
  COMPONENT Devel
)

write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfigVersion.cmake"
  VERSION ${xTests_VERSION}
  COMPATIBILITY AnyNewerVersion
)
export(TARGETS xTests
  FILE "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsTargets.cmake"
  NAMESPACE xTests::
)
set(PACKAGE_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")
configure_file(cmake/xTestsConfig.cmake.in
  "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfig.cmake"
  @ONLY
)
export(PACKAGE xTests)

set(ConfigPackageLocation cmake/xTests)
install( EXPORT xTestsTargets
  FILE xTestsTargets.cmake
  NAMESPACE xTests::
  DESTINATION ${ConfigPackageLocation}
)
install( FILES
    "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfigVersion.cmake"
  DESTINATION ${ConfigPackageLocation}
  COMPONENT Devel
)

