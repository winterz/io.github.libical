+++
title = "Quick Start"
description = "One page summary of how to start."
date = 2021-05-01T08:20:00+00:00
updated = 2021-05-01T08:20:00+00:00
draft = false
weight = 20
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "One page summary of how to start."
toc = true
top = false
+++

Please see the comments at the top of CMakeLists.txt for
the available configuration options you can pass to cmake.

The installation directory defaults to `/usr/local` on UNIX
and `C:/Program Files` on Windows.  You can change this by
passing `-DCMAKE_INSTALL_PREFIX=/install/path` to cmake.

To build a debug version pass `-DCMAKE_BUILD_TYPE=Debug` to cmake.

## Requirements

To build libical you will need:
 - a C99-compliant C compiler (let us know if the build fails with your C compiler)
 - a C11-compliant C compiler for libical-glib
 - a C++11 compliant compiler for C++ bindings
 - CMake version 3.20.0 or higher
 - Perl
 - libicu (not required but strongly recommended)

## Building

### On Unix with gcc or clang

```
mkdir build
cd build
cmake ..
make
make install
```

### On Windows with MicroSoft Visual Studio

From a command prompt for the version of MSVC you want to use
```bash
mkdir build
cd build
cmake -G "NMake Makefiles" ..
nmake
nmake install
```

NOTE: Some MSVC 32bit compilers (like MSVC2005) use a 64bit version of time_t.
In these cases you must pass `-DUSE_32BIT_TIME_T=true` to cmake to make sure
the 32bit version of time_t is used instead.

### On Windows with mingw
Make sure you have the path to the MinGW programs in %PATH% first, for example:
```bash
set "PATH=c:\MinGW\mingw64\bin;%PATH%"
mkdir build
cd build
cmake -G "MinGW Makefiles" ..
mingw32-make
mingw32-make install
```

### On Windows under Cygwin
```bash
mkdir build
cd build
cmake ..
make
make install
```

### On MSYS with mingw
```bash
mkdir build
cd build
cmake -G "MSYS Makefiles" ..
nmake
nmake install
```

To run the test suite, from inside the build directory
run `make test` (or `nmake test` or `mingw32-make test`)

To run the test suite in verbose mode, pass `ARGS="-V"` to the make command
For example: `nmake test ARGS="-V"`

By default, the buildsystem creates shared(dynamic) and static versions
of the libraries, but that behavior can be modified at CMake time:
 - To build the static libraries only, pass `-DSTATIC_ONLY=True` to CMake.
 - To build the shared libraries only, pass `-DSHARED_ONLY=True` to CMake.

## Dealing with Dependencies

You can force CMake to ignore an optional dependencies passing the option as defined in CMakeLists.txt like `-DCMAKE_DISABLE_FIND_PACKAGE_{PACKAGE}=True`.

For instance:

```bash
# tell cmake to ignore ICU
cmake -DCMAKE_DISABLE_FIND_PACKAGE_ICU=True
```
