# declare the name of the project
project(ExtendedKF)

#Specify the version being used as well as the language
cmake_minimum_required (VERSION 3.5)

#Setting language standard
set(CMAKE_CXX_STANDARD 11)  # enable C++11 standard
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -g -O2")

#Add “-g -O2” options to the gcc compiler
#add_compile_options(-std=c++11)

#Specifying header search paths
#Header search paths are important for both the compiler (so that it knows where to search for headers) but also for CLion,
#since the IDE can index the relevant directories and provide code completion and navigation facilities on #include statements.
include_directories(include)
include_directories(Eigen)

#create text variables
set(sources
    #Here comment `src/FusionEKF.cpp` just for `add_library` example
    #src/FusionEKF.cpp
    src/kalman_filter.cpp
    src/main.cpp
    src/tools.cpp)

# Destination path for the lib
#CMAKE_ARCHIVE_OUTPUT_DIRECTORY sets where static (archive) libraries (.a files on Linux) will be built. It doesn't affect where install puts files
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY  ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

#build a library
add_library(FusionEKF STATIC src/FusionEKF.cpp)


##create an executable binary
add_executable(ExtendedKF ${sources})
##link an executable to the located library
target_link_libraries(ExtendedKF FusionEKF)
##Note, that target_link_libraries() shall be placed after add_executable() command.

#specify install base directory path
set(CMAKE_INSTALL_PREFIX ../app)    # relative to where `make install` is executated
install(TARGETS ExtendedKF DESTINATION bin)

install(FILES ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}/libFusionEKF.a DESTINATION lib)

