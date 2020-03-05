---
title: CMake
layout: main
---

Introduction
============
[CMake](https://cmake.org) is a tool to build, test and package software independently from an operating system.

New CMake users are advised to follow the "An Introduction to Modern CMake" tutorial, CMake 2.x users may be interested in "It's Time To Do CMake Right" (see references below).

The underlying concepts used in our cmake implementation can be found [here](https://github.com/AliceO2Group/AliceO2/blob/dev/doc/CMakeInstructions.md).

Modern CMake
============

_Modern CMake_ promotes, among others, following concepts:
- Use `CONFIG` mode to load dependency settings to the project, if not available `Find<package>.cmake` recipe should provide imported target
- Use [targets](https://gitlab.kitware.com/cmake/community/wikis/doc/tutorials/Exporting-and-Importing-Targets) and properties, avoid operations on directories and global variables
  - Use target property scopes: `PRIVATE` and `INTERFACE`
  - Instead of setting a global variable use target specific functions: `target_compile_options`, `target_compile_features` or `target_compile_definitions`
- [Generator expressions](https://cmake.org/cmake/help/latest/manual/cmake-generator-expressions.7.html) should be used to replace simple `if`/`else` statements
- Export your targets by creating [CMake config](https://gitlab.kitware.com/cmake/community/wikis/doc/tutorials/Exporting-and-Importing-Targets#exporting-targets)


References
=========
1. [An Introduction to Modern CMake](https://cliutils.gitlab.io/modern-cmake/)
2. [It's Time To Do CMake Right](https://pabloariasal.github.io/2018/02/19/its-time-to-do-cmake-right/)
3. [O2 CMake](https://github.com/AliceO2Group/AliceO2/blob/dev/doc/CMakeInstructions.md)
