include_directories (${STLSoft_INCLUDE_DIRS})

add_library(xTests xtests.core.cpp)
set_target_properties(xTests PROPERTIES OUTPUT_NAME "xtests.core")
target_include_directories(xTests
    PRIVATE
        ${CMAKE_SOURCE_DIR}/include
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>)

install(TARGETS xTests
    EXPORT project-targets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

