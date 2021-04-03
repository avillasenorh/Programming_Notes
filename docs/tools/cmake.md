# CMake


Python: needed for testing (?)
BLAS and LAPACK
MPI (OpenMPI)
Eigen linear algebra template library
Boost libraries (Filesystem, Python & Test)


Eigen

    $ cd
    $ cd src
    $ mkdir -p eigen
    $ curl -Ls http://bitbucket.org/eigen/eigen/get/3.3.4.tar.gz | tar -xz -C eigen --strip-components=1
    $ CC=gcc FC=gfortran cmake -H. -Bbuild_eigen -DCMAKE_INSTALL_PREFIX="$HOME/src/eigen"
    [lots of warning, errors?]

Get information:

    $ cmake --help
    $ cmake --build . --target help
    $ cmake --system-information [logfile] # lots of output, so better write to a file
    $ cmake --build build_eigen -- install > install.log 2> install.err

Generators:

Makefiles, Ninja, Visual Studio, ...

```
$ cmake --help
.
.
.
Generators

The following generators are available on this platform:
  Unix Makefiles               = Generates standard UNIX makefiles.
  Ninja                        = Generates build.ninja files.
  Xcode                        = Generate Xcode project files.
  CodeBlocks - Ninja           = Generates CodeBlocks project files.
  CodeBlocks - Unix Makefiles  = Generates CodeBlocks project files.
  CodeLite - Ninja             = Generates CodeLite project files.
  CodeLite - Unix Makefiles    = Generates CodeLite project files.
  Sublime Text 2 - Ninja       = Generates Sublime Text 2 project files.
  Sublime Text 2 - Unix Makefiles
                               = Generates Sublime Text 2 project files.
  Kate - Ninja                 = Generates Kate project files.
  Kate - Unix Makefiles        = Generates Kate project files.
  Eclipse CDT4 - Ninja         = Generates Eclipse CDT 4.0 project files.
  Eclipse CDT4 - Unix Makefiles= Generates Eclipse CDT 4.0 project files.
```


Minimum `CMakeLists.txt`:

    cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
    project(test_project LANGUAGES CXX)
    add_executable(hello-world hello-world.cpp)

Commands for "in-source" build:

    $ cmake .
    $ cmake --build .

Commands for "out-of-source" build:

    $ mkdir -p build && cd build
    $ cmake ..
    $ cmake --build .

[non-standard alternative from "root" directory: $ cmake -H. -Bbuild ]


Options for "build"

```
$ cmake --build . --target help
The following are some of the valid targets for this Makefile:
... all (the default if no target is provided)
... clean
... depend
... rebuild_cache
... edit_cache
... getjul                      # this is one of the executables defined in CMakeLists.txt
```

[for more advanced projects, also "test", "install", and "package" ]

How to invoke explicitly a generator:

    $ cmake -G Ninja ..

Link with a static library:

    add_library(library_name STATIC header_files.hpp source_files.cpp)
    target_link_libraries(executable library_name)

Build directory will contain: lib{library_name}.a

Possible values:
STATIC
SHARED
OBJECT
MODULE

IMPORTED    = a library located outside the project (e.g. FFTW3?)
INTERFACE
ALIAS

Define, set and output variables:

    set(USE_LIBRARY OFF)
    message(STATUS "Compile sources into a library? ${USE_LIBRARY}")
    message("Compile sources into a library? ${USE_LIBRARY}")

```console
$ cmake .
.
.
.
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Compile sources into a library? OFF
Compile sources into a library? OFF
-- Configuring done
-- Generating done
...
```


Specifying compiler:

    $ cmake -D CMAKE_CXX_COMPILER=clang++ ...   # recommended !!!

or

    $ env CXX=clang++ cmake ...

but also inside `CMakeLists.txt`

    set(CMAKE_CXX_COMPILER "/usr/local/bin/g++")  # before defining project!!!


Build types:

Debug, Release, RelWithDebInfo, MinSizeRel

    set(CMAKE_BUILD_TYPE Debug)

or

    $ cmake -D CMAKE_BUILD_TYPE=Debug ...



Set compiler and compiler options:


OPTIONS:

    list(APPEND flags "-fPIC" "-Wall")
    add_library(library_name STATIC header_files.hpp source_files.cpp)
    target_compile_options(library_name PRIVATE ${flags})
    target_compile_options(execuatable_name PRIVATE "-fPIC")

    target_link_libraries(executable_name library_name)

    set_target_properties(animals PROPERTIES CXX_STANDARD 14 CXX_EXTENSIONS OFF CXX_STANDARD_REQUIRED ON POSITION_INDEPENDENT_CODE 1)

also

    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_EXTENSIONS OFF)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)

Discovering system information:

- Compiler ID
- Processor architecture
- Processor instruction set


    message(STATUS "Configuring on/for ${CMAKE_SYSTEM_NAME}")  # must be after "project"!!!


    CMAKE_CXX_COMPILER_ID


    find_package(Eigen3 3.3 REQUIRED CONFIG)

