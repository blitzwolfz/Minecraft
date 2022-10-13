cmake_minimum_required(VERSION 3.23)

if(${CMAKE_VERSION} VERSION_LESS 3.23)
    cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
endif()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS_RELEASE "-O3")

message(${CMAKE_CURRENT_SOURCE_DIR})

project(Minecraft)

set(CMAKE_CXX_STANDARD 20)
set (CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_VERBOSE_MAKEFILE TRUE)


# Makes it easier to add source files
include_directories(./libraries)
include_directories(./libraries/include)
include_directories(./libraries/include)
set(SOURCE_FILES ./src/main.cpp ./src/glad.c)

add_executable(Minecraft ${SOURCE_FILES})

# For future use for cross comp
if (WIN32)
    add_library(glfw3 STATIC IMPORTED)
    add_library(glfw3::glfw3 ALIAS glfw3)
    target_include_directories(glfw3 INTERFACE ${CMAKE_SOURCE_DIR}/libraries/include/GLFW)
    set_target_properties(glfw3 PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libraries/lib/glfw3.lib)
    target_link_libraries(Minecraft glfw3::glfw3)
endif ()

