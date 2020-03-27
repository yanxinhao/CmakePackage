cmake_minimum_required(VERSION 3.0.0)
project(mylib VERSION 0.1.0)
add_library(mylib mylib.cpp include/mylib.h)
SET(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR}/install)
target_include_directories(mylib PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)
set_target_properties(mylib PROPERTIES PUBLIC_HEADER "include/mylib.h")
install(TARGETS mylib
    EXPORT mylib-targets
    PUBLIC_HEADER DESTINATION include
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin)
install(EXPORT mylib-targets
    NAMESPACE mylib::
    FILE mylib-config.cmake
    DESTINATION lib/cmake/mylib)