cmake_minimum_required(VERSION 3.10)

# Set the project name
project(mistry-slicer)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)  # Ensure the specified standard is used

# Include directories for headers
if(WIN32)
    # Include the directory that contains unistd.h
    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include/unistd_h)
endif()

# Always include the main headers
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# Find all .cpp files in the src directory and set them as source files
file(GLOB_RECURSE SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
)

# Determine build type if not set
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

# Define compile definitions based on build type
if(CMAKE_BUILD_TYPE MATCHES "Debug")
    add_compile_definitions(DEBUG)
elseif(CMAKE_BUILD_TYPE MATCHES "Release")
    add_compile_definitions(RELEASE)
endif()

# Create the library
add_library(${PROJECT_NAME} STATIC ${SOURCES})

