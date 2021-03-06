# CMAKE EXAMPLE
- Project tree
```bash
cmake_practice/
├── CMakeLists.txt
├── data
├── Docs
├── Eigen
│   ├── Array
│   ├── Cholesky
│   ├── CholmodSupport
│   ├── CMakeLists.txt
│   ├── Core
│   ├── Dense
│   ├── Eigen
│   ├── Eigen2Support
│   ├── Eigenvalues
│   ├── Geometry
│   ├── Householder
│   ├── IterativeLinearSolvers
│   ├── Jacobi
│   ├── LeastSquares
│   ├── LU
│   ├── MetisSupport
│   ├── OrderingMethods
│   ├── PardisoSupport
│   ├── PaStiXSupport
│   ├── QR
│   ├── QtAlignedMalloc
│   ├── Sparse
│   ├── SparseCholesky
│   ├── SparseCore
│   ├── SparseLU
│   ├── SparseQR
│   ├── SPQRSupport
│   ├── src
│   |   └── ...
│   ├── StdList
│   ├── StdVector
│   ├── SuperLUSupport
│   ├── SVD
│   └── UmfPackSupport
├── img
├── include
│   ├── FusionEKF.h
│   ├── ground_truth_package.h
│   ├── kalman_filter.h
│   ├── measurement_package.h
│   └── tools.h
├── README.md
├── src
│   ├── FusionEKF.cpp
│   ├── kalman_filter.cpp
│   ├── main.cpp
│   └── tools.cpp
└── tutorial
```

<br>

`CMakeLists.txt`

```cmake
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
#without directory, `${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/ExtendedKF` is INVALID
install(TARGETS ExtendedKF DESTINATION bin)
#with directory
install(FILES ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}/libFusionEKF.a DESTINATION lib)
```

# Credits

- [cmake tutorial](tutorial)
- [ndrplz/self-driving-car/project_6_extended_kalman_filter](https://github.com/ndrplz/self-driving-car/tree/master/project_6_extended_kalman_filter)

---

## [cmake-demo](https://github.com/wzpan/cmake-demo/tree/89110ffcc5989eb9ac53cb4fcb66fa31af914f50)

=============================================================================================
# Extended Kalman Filter Project
Self-Driving Car Engineer Nanodegree Program

## Project Description

This code implements the extended Kalman filter in C++. We are providing simulated lidar and radar measurements detecting a bicycle that travels around your vehicle. You will use a Kalman filter, lidar measurements and radar measurements to track the bicycle's position and velocity.

---

## Dependencies

* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it: `./ExtendedKF path/to/input.txt path/to/output.txt`. You can find
   some sample inputs in 'data/'.
    - eg. `./ExtendedKF ../data/sample-laser-radar-measurement-data-1.txt output.txt`

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

