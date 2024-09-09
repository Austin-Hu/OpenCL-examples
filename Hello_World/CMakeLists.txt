# ##############################################################################
# Copyright (C) Intel Corporation
#
# SPDX-License-Identifier: MIT
# ##############################################################################
cmake_minimum_required(VERSION 3.15)
project(Hello_World)

# Default install places 64 bit runtimes in the environment, so we want to do a
# 64 bit build by default.
if(WIN32)
    if(NOT DEFINED CMAKE_GENERATOR_PLATFORM)
      set(CMAKE_GENERATOR_PLATFORM
          x64
          CACHE STRING "")
      message(STATUS "Generator Platform set to ${CMAKE_GENERATOR_PLATFORM}")
    endif()
endif()

find_package(OpenCL CONFIG REQUIRED)

set(TARGET Hello_World)
set(SOURCES hello.c)

# Set a default build type if none is specified for a single-config generator
if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
      message(STATUS "Setting the build type to '${DEFAULT_BUILD_TYPE}' as none was specified.")
      set(CMAKE_BUILD_TYPE "${DEFAULT_BUILD_TYPE}" CACHE STRING "Choose the type of build." FORCE)
endif ()

add_executable(${TARGET} ${SOURCES})

target_link_libraries(${TARGET}
    PRIVATE
    OpenCL::OpenCL
    OpenCL::Headers
    OpenCL::HeadersCpp
    OpenCL::Utils
    OpenCL::UtilsCpp
)

