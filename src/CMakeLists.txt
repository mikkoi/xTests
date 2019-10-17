add_library(xTests.core xtests.core.cpp)
target_link_libraries(xTests.core STLSoft::STLSoft)
set_target_properties(xTests.core PROPERTIES
    OUTPUT_NAME "xtests"
    PUBLIC_HEADER "${CMAKE_SOURCE_DIR}/include/xtests/xtests.h;${CMAKE_SOURCE_DIR}/include/xtests/test/util/compiler_warnings_suppression.last_include.h;${CMAKE_SOURCE_DIR}/include/xtests/test/util/compiler_warnings_suppression.first_include.h;${CMAKE_SOURCE_DIR}/include/xtests/util/filesystem_exception.hpp;${CMAKE_SOURCE_DIR}/include/xtests/util/temp_directory.hpp;${CMAKE_SOURCE_DIR}/include/xtests/util/temp_file.hpp")
target_include_directories(xTests.core PUBLIC
    $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)

install(TARGETS xTests.core
    EXPORT project-targets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/xtests
)
