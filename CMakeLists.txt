cmake_minimum_required (VERSION 3.16 FATAL_ERROR)
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "")
endif()

project(cmake-projects-test LANGUAGES CXX)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR} CACHE PATH "Set install prefix to project source folder." FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

set(LibA_SOURCE_DIR ${PROJECT_SOURCE_DIR}/lib_a)
list(APPEND CMAKE_PREFIX_PATH ${LibA_SOURCE_DIR}/cmake)
include(${CMAKE_ROOT}/Modules/ExternalProject.cmake)
ExternalProject_Add(LibA
  SOURCE_DIR ${LibA_SOURCE_DIR}
  )

set(LibB_SOURCE_DIR ${PROJECT_SOURCE_DIR}/lib_b)
list(APPEND CMAKE_PREFIX_PATH ${LibB_SOURCE_DIR}/cmake)
include(${CMAKE_ROOT}/Modules/ExternalProject.cmake)
ExternalProject_Add(LibB
  SOURCE_DIR ${LibB_SOURCE_DIR}
  )

add_subdirectory(app)

