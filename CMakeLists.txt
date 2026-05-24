cmake_minimum_required(VERSION 3.10)
project(GH-Offset-Dumper)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add definitions for Windows
if(WIN32)
    add_definitions(-DUNICODE -D_UNICODE)
endif()

add_subdirectory(src/dumper-lib)
add_subdirectory(src/dumper)
