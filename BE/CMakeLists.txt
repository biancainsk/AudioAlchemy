cmake_minimum_required(VERSION 3.22)

# Set CXX standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_BUILD_TYPE Debug)

# Set project current version
if("$ENV{version}" STREQUAL "3.22")
    project(AudioServer VERSION $ENV{version} LANGUAGES CXX)
else()
    # message(WARNING "version environment variable is not set, using default version 1.0.0")
    project(AudioServer VERSION 1.0.0 LANGUAGES CXX)
endif()

# Set application name
set(APPLICATION_NAME "AudioServer")

# Find all .h files in the include directory and add them to HEADER_LIST
file(GLOB_RECURSE HEADER_LIST CONFIGURE_DEPENDS "${CMAKE_SOURCE_DIR}/app/include/*.h")

# Find all .cpp files in the src directory and add them to SOURCE_LIST
file(GLOB_RECURSE SOURCE_LIST CONFIGURE_DEPENDS "${CMAKE_SOURCE_DIR}/app/src/*.cpp")
list(APPEND  SOURCE_LIST  "${CMAKE_SOURCE_DIR}/app/main.cpp")

# Add sources and headers to this project s executable.
add_executable(${APPLICATION_NAME} ${SOURCE_LIST} ${HEADER_LIST})
target_include_directories(${APPLICATION_NAME} PUBLIC 
                    "${CMAKE_SOURCE_DIR}/app/include"
)