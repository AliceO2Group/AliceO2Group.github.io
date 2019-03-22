---
title: CMake - WIP
layout: main
---

Introduction
------------
[CMake](https://cmake.org) is a tool to build, test and package software independent from an operating system.


Modern CMake
------------
O<sup>2</sup> follows so-called modern CMake that promotes, among others, following concepts:
- If dependency does not provide a target in its CMake config, `Find<package>.cmake` should do it instead
- Configuration should be done on [target](https://gitlab.kitware.com/cmake/community/wikis/doc/tutorials/Exporting-and-Importing-Targets) basis (no operations on directories and global variables)
- [Generator expressions](https://cmake.org/cmake/help/latest/manual/cmake-generator-expressions.7.html) should be used to replace simple `if`/`else` statements
- Each package should [export CMake config](https://gitlab.kitware.com/cmake/community/wikis/doc/tutorials/Exporting-and-Importing-Targets#exporting-targets)


Refereces
---------
1. [It's Time To Do CMake Right](https://pabloariasal.github.io/2018/02/19/its-time-to-do-cmake-right/)
