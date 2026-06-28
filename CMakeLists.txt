cmake_minimum_required(VERSION 3.15)

project(GreenEngine C CXX)

# Settings
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Android/Linux Build Definitions
if(ANDROID)
    add_definitions(-DANDROID -DLINUX -DPOSIX -D_GNU_SOURCE)
    message(STATUS "Configuring build for Android")
endif()

# Global include directories
include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    ${CMAKE_CURRENT_SOURCE_DIR}/src
)

# --- Modules Orchestration ---

# Include gmod-module-base if it exists
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/gmod-module-base/CMakeLists.txt")
    add_subdirectory(gmod-module-base)
    message(STATUS "gmod-module-base included")
else()
    message(WARNING "gmod-module-base not found")
endif()

# Include garrysmod logic if it exists
if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/garrysmod/CMakeLists.txt")
    add_subdirectory(garrysmod)
    message(STATUS "garrysmod logic included")
else()
    message(WARNING "garrysmod directory not found")
endif()

# --- Build targets ---

# If you have a main entry point for the engine, define it here
# Example:
# add_executable(green_engine main.cpp)
# target_link_libraries(green_engine PRIVATE gmod_module_base)

message(STATUS "Master CMake configuration completed successfully")
