cmake_minimum_required(VERSION 3.9)
project(toy_bin VERSION 1.0.1 DESCRIPTION "toy_bin description")
include(GNUInstallDirs)
add_executable(toy_bin main.cpp)
set_target_properties(toy_bin PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION 1)
configure_file(toy_bin.pc.in toy_bin.pc @ONLY)

find_package(toy_lib REQUIRED CONFIG)

message(STATUS "INC DIRS" ${toy_lib_INCLUDE_DIR})
target_include_directories(toy_bin
                            PUBLIC
                           ${toy_lib_INCLUDE_DIR}
                           $<BUILD_INTERFACE:${toy_lib_INCLUDE_DIR}>
                           $<INSTALL_INTERFACE:include>)

target_link_libraries(toy_bin ${toy_lib_LIBRARY})


# target_include_directories(toy_bin PRIVATE include)
install(TARGETS toy_bin
    ARCHIVE DESTINATION ${CMAKE_INSTALL_BINDIR})

# install(FILES ${CMAKE_BINARY_DIR}/toy_bin.pc
#     DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)