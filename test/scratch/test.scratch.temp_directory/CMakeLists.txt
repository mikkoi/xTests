if(WIN32)
    add_executable(test.scratch.temp_directory test.scratch.temp_directory.cpp)
    target_link_libraries(test.scratch.temp_directory xTests.core STLSoft::STLSoft)
    add_test(NAME test.scratch.temp_directory COMMAND ./test.scratch.temp_directory)
endif()

