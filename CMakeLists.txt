cmake_minimum_required(VERSION 3.4)

project(alglib)

file(GLOB headers "alglib/src/*.h")
file(GLOB sources "alglib/src/*.cpp")

add_library(alglib ${headers} ${sources})

include(GNUInstallDirs)
target_include_directories(alglib
  PUBLIC
  "$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/alglib/src>"
  "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>")

set_target_properties(alglib
  PROPERTIES
  PUBLIC_HEADER "${headers}")

install(TARGETS alglib
        EXPORT alglib
        COMPONENT runtime
        RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}" COMPONENT bin
        LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}" COMPONENT lib
        ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}" COMPONENT lib
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/alglib)
