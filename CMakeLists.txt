cmake_minimum_required (VERSION 3.16 FATAL_ERROR)
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
endif()

project(cmake-projects-test LANGUAGES CXX)

#message(PROJECT_SOURCE_DIR\ ${PROJECT_SOURCE_DIR})

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR} CACHE PATH "Set install prefix to project source folder." FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

#message(CMAKE_INSTALL_PREFIX\ ${CMAKE_INSTALL_PREFIX})

add_subdirectory(lib_a)
#TODO Must perform library installation.
list(APPEND CMAKE_PREFIX_PATH ${LibA_SOURCE_DIR}/cmake)
find_package(LibALib)

#message(PREFIX_PATH\ ${CMAKE_PREFIX_PATH})

add_subdirectory(app)

