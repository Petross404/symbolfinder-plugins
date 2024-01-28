cmake_minimum_required(VERSION 3.0)

project(symbolfinder-plugins VERSION 0.0.1)

#Set the language standard.
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(GNUInstallDirs)
include(FindDoxygen)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed.
set(CMAKE_AUTOMOC ON)
# Instruct CMake to create code from Qt ui files
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

#Set this variable so it can save the conan.cmake
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules")

include(GNUInstallDirs)
#include("${CMAKE_MODULE_PATH}/Sanitizers.cmake")
include("${CMAKE_MODULE_PATH}/ClangFormat.cmake")
#include("${CMAKE_MODULE_PATH}/ClangTidy.cmake")
#include("${CMAKE_MODULE_PATH}/Configure.cmake")
#include("${CMAKE_MODULE_PATH}/IncludeUse.cmake")
#include("${CMAKE_MODULE_PATH}/BuildDoc.cmake")

handle_dependency_clang_format()

# Find the QtWidgets library
find_package(Qt5 COMPONENTS Core Widgets Gui CONFIG REQUIRED)

add_subdirectory(src/nmdriver)
add_subdirectory(src/scanelfdriver)

foreach(plugin ${Qt5Gui_PLUGINS})
  get_target_property(_loc ${plugin} LOCATION)
  message("Core Plugin ${plugin} is at location ${_loc}")
endforeach()
