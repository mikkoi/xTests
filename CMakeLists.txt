cmake_minimum_required(VERSION 3.9 FATAL_ERROR)
if(POLICY CMP0074)
    cmake_policy(SET CMP0074 NEW) # Use <PackageName>_ROOT variables
endif()
project(xTests
    DESCRIPTION "Simple, easy-to-use, efficient testing library, for C, C++. It's not particularly great, but it's small and portable enough to be bundled with other, more important, libraries."
    LANGUAGES C CXX)

# Directory for CMake specific extensions and source files.
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

# Set build type to Debug if this is a Git repository.
# Otherwise set to Release.
# Unless user overrides on the command line.
include(BuildType)

# Configure a project for testing with CTest/CDash
# and activate testing (set var BUILD_TESTING=On).
# Unless user overrides on the command line.
include(CTest)

# Handle version number
set(RX_WS "[ \t\r\n]")
file(READ "${CMAKE_CURRENT_SOURCE_DIR}/include/xtests/xtests.h" _header_file)
string(REGEX MATCH "#define${RX_WS}+_XTESTS_VER_MAJOR${RX_WS}+([0-9]+)" MAJOR_DUMMY ${_header_file})
set(_VERSION_MAJOR ${CMAKE_MATCH_1})
string(REGEX MATCH "#define${RX_WS}+_XTESTS_VER_MINOR${RX_WS}+([0-9]+)" MINOR_DUMMY ${_header_file})
set(_VERSION_MINOR ${CMAKE_MATCH_1})
string(REGEX MATCH "#define${RX_WS}+_XTESTS_VER_REVISION${RX_WS}+([0-9]+)" PATCH_DUMMY ${_header_file})
set(_VERSION_PATCH ${CMAKE_MATCH_1})

# Set project version number here
set(PROJECT_VERSION_MAJOR ${_VERSION_MAJOR})
set(PROJECT_VERSION_MINOR ${_VERSION_MINOR})
set(PROJECT_VERSION_PATCH ${_VERSION_PATCH})
set(PROJECT_VERSION "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}")

# Adhere strictly to C and C++ standards plus extensions.
set(CMAKE_C_STANDARD 90)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON) # GNU extensions and POSIX standard
set(CMAKE_CXX_STANDARD 98)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)

# Assuming test library will always be linked statically.
set( BUILD_SHARED_LIBS FALSE )

# #########################################################
# Preparations for installing

# Provides install directory variables as defined by the GNU Coding Standards.
include(GNUInstallDirs)

# Build

find_package(STLSoft 1.9.125 REQUIRED)

add_subdirectory(src)

# Tests
if(BUILD_TESTING)
    add_subdirectory(test)
endif()

# Examples
add_subdirectory(examples)

# build target 'docs' for Doxygen generated documents.
# add_subdirectory( docs EXCLUDE_FROM_ALL )

# #########################################################
# Export and install the project

string(TOLOWER ${PROJECT_NAME} EXPORT_NAME)

# Prepare a config and config-version files
include(CMakePackageConfigHelpers)
configure_package_config_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/cmake/${EXPORT_NAME}-config.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/cmake/${EXPORT_NAME}-config.cmake
  INSTALL_DESTINATION ${LIB_INSTALL_DIR}/${EXPORT_NAME}/cmake
)
write_basic_package_version_file(
  ${CMAKE_CURRENT_BINARY_DIR}/cmake/${EXPORT_NAME}-config-version.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY AnyNewerVersion
)

export(EXPORT project-targets
    FILE "${CMAKE_CURRENT_BINARY_DIR}/cmake/${EXPORT_NAME}-targets.cmake"
    NAMESPACE "${PROJECT_NAME}::"
)

# Install to GNU type subdirs under CMAKE_INSTALL_PREFIX
install(EXPORT project-targets
    NAMESPACE "${PROJECT_NAME}::"
    FILE "${EXPORT_NAME}-targets.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${EXPORT_NAME}
)
install( FILES
    "${CMAKE_CURRENT_BINARY_DIR}/cmake/${EXPORT_NAME}-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake/${EXPORT_NAME}-config-version.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${EXPORT_NAME}
)

# Store the current build directory in the CMake
# user package registry for package.
# This helps dependent projects use a package
# from the current project’s build tree,
# i.e. without installing it.
export(PACKAGE "${PROJECT_NAME}")
























# include( GenerateExportHeader )
# include( CMakePackageConfigHelpers )

# add_library( xTests src/xtests.core.cpp )
# generate_export_header (xTests )
# set_property( TARGET xTests PROPERTY VERSION ${xTests_VERSION} )
# set_property( TARGET xTests PROPERTY INTERFACE_xTests_MAJOR_VERSION ${xTests_VERSION} )
# set_property( TARGET xTests APPEND PROPERTY
#   COMPATIBLE_INTERFACE_STRING xTests_MAJOR_VERSION
# )
#
# install( TARGETS xTests EXPORT xTestsTargets
#   LIBRARY DESTINATION lib
#   ARCHIVE DESTINATION lib
#   RUNTIME DESTINATION bin
# )
# install( DIRECTORY
#     "${CMAKE_CURRENT_SOURCE_DIR}/include/xtests"
#   DESTINATION include
#   COMPONENT Devel
# )
#
# write_basic_package_version_file(
#   "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfigVersion.cmake"
#   VERSION ${xTests_VERSION}
#   COMPATIBILITY AnyNewerVersion
# )
# export(TARGETS xTests
#   FILE "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsTargets.cmake"
#   NAMESPACE xTests::
# )
# set(PACKAGE_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/include")
# configure_file(cmake/xTestsConfig.cmake.in
#   "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfig.cmake"
#   @ONLY
# )
# export( PACKAGE xTests )
#
# set( ConfigPackageLocation cmake/xTests )
# install( EXPORT xTestsTargets
#   FILE xTestsTargets.cmake
#   NAMESPACE xTests::
#   DESTINATION ${ConfigPackageLocation}
# )
# install( FILES
#     "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfig.cmake"
#     "${CMAKE_CURRENT_BINARY_DIR}/cmake/xTestsConfigVersion.cmake"
#   DESTINATION ${ConfigPackageLocation}
#   COMPONENT Devel
# )

