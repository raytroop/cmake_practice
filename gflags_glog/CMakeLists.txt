# CMake looks for build instructions in a file called CMakeLists.txt. Always
# start the top level CMakeLists.txt with the minimum required CMake version.
# This hints to the build system and future developers which features are
# currently in use.

# CMake version 3.0 or higher is required for the Hunter package manager.
cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_STANDARD 11)

# Pick a good name for the project, but you can always change it later.
project(codecast002)

set(CMAKE_MODULE_PATH "${OpenCV_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
find_package(gflags CONFIG REQUIRED)
find_package(glog CONFIG REQUIRED)

# An executable target will create a binary for our new app.
add_executable(codecast002
        codecast002_main.cc)
target_link_libraries(codecast002
        glog::glog
        gflags)
