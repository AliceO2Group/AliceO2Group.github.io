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
3. Go to the directory from where you would usually run CLion.
4. Create a new file ".envrc" which loads all the build environments of the projects that you will run on CLion. Use <your_path_to>/alice/sw/BUILD/O2-latest/O2/.envrc as a starting point. [See below](#.envrc) for an example.
5. Run `direnv allow`.
6. Run `clion`.
7. If you haven't opened your project, go to File->Open. Choose your project's directory. It should compile out of the box.

Notes

1. **Options** - By default, no CMake options are needed in "File->Settings->Build, Execution, Deployment->CMake->CMake options". However, when "install" is added to the "Build options", a valid CMAKE_INSTALL_PREFIX has to be added in "CMake options", for example "-DCMAKE_INSTALL_PREFIX=/home/<user_name>/alice/sw/slc7_x86-64/O2/latest".
2. **Mac clion exe** - On Mac the path to the clion executable can either be `/Applications/CLion.app/Contents/MacOS` or `~/Library/Application\ Support/JetBrains/Toolbox/apps/CLion/ch-0/201.5616.31/CLion\ 2020.1\ EAP.app/Contents/MacOS/clion` (adapt the version numbers) if installed with Jetbrains Toolbox.
3. **Pre-existing projects** - For projects that already existed, it is better to remove them by deleting the folder `.idea` in the source directory.

.envrc
------
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

Full Remote Mode
----------------

1. Setup the remote host for alibuild
2. Run aliBuild on the remote host as usual
5. Append the following in ~/.bashrc
```
 export ALIBUILD_WORK_DIR="/home/$USER/alice/sw"
 WORK_DIR=$ALIBUILD_WORK_DIR
 source /home/$USER/alice/sw/slc8_x86-64/QualityControl/latest/etc/profile.d/init.sh  # Replace with your package
```
6. Follow the instructions from [here](https://www.jetbrains.com/help/clion/remote-projects-support.html) to start a full remote project on CLion running on your local host, with the options outlined below. 

  Toolchain (Addresses on remote host)
  - ssh://clion@$HOSTNAME:22
  - gcc: `/home/$USER/alice/sw/slc8_x86-64/GCC-Toolchain/latest/bin/gcc`
  - g++: `/home/$USER/alice/sw/slc8_x86-64/GCC-Toolchain/latest/bin/g++`
  - gdb: `/home/$USER/alice/sw/slc8_x86-64/GCC-Toolchain/latest/bin/gdb`
  
  CMake
  - Toolchain: the name of the toolchain just created
  - CMake options: `-DLLVM_ROOT=/home/$USER/alice/sw/slc8_x86-64/Clang/latest  -DLIBJALIENO2=/home/$USER/alice/sw/slc8_x86-64/libjalienO2/latest`
7. Load CMake Project
8. Build / Run


Editor
------

Coding guidelines can be applied by using a special settings file. See [here](https://github.com/AliceO2Group/CodingGuidelines#clion).
