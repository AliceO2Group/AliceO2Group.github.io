---
title: IDE support
layout: main
---

CLion
=====

Compilation
-----------

1. Install [`direnv`](https://direnv.net/docs/installation.html).
2. Build with aliBuild as you would do normally.
3. Go to the directory where you run CLion.
4. Create a new file ".envrc" which loads all the build environments of the projects that you will run on CLion. Use <your_path_to>/alice/sw/BUILD/O2-latest/O2/.envrc as a starting point. For example:
```
# Source the build environment which was used for this package
WORK_DIR=<your_path_to>/alice/sw
source $WORK_DIR/slc7_x86-64/O2/latest/etc/profile.d/init.sh
source $WORK_DIR/slc7_x86-64/QualityControl/latest/etc/profile.d/init.sh
source_up

# On mac we build with the proper installation relative RPATH,
# so this is not actually used and it's actually harmful since
# startup time is reduced a lot by the extra overhead from the 
# dynamic loader
unset DYLD_LIBRARY_PATH
```
5. Run `direnv allow`.
6. Run `clion`.
7. If you haven't opened your project, go to File->Open. Choose your project's directory. It should compile out of the box.

By default, no CMake options are needed in "File->Settings->Build, Execution, Deployment->CMake->CMake options". However, when "install" is added to the "Build options", a valid CMAKE_INSTALL_PREFIX has to be added in "CMake options", for example "-DCMAKE_INSTALL_PREFIX=/home/<user_name>/alice/sw/slc7_x86-64/O2/latest".

Editor
------

Coding guidelines can be applied by using a special settings file. See [here](https://github.com/AliceO2Group/CodingGuidelines#clion).
