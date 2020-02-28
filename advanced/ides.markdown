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

Full Remote Mode
----------------

1a. Install cmake3 on the remote host
```
yum -y install cmake3
```

1b. Install devtoolset on the remote host
```
yum install -y centos-release-scl
yum-config-manager --enable rhel-server-rhscl-7-rpms
yum install -y devtoolset-7
```
1c. Make sure rsync is installed on the remote and local host.
```
yum -y install rsync
#install rsync on local host
```
2. Run aliBuild on the remote host as usual
3. Create a new clion user (as root)
```
useradd clion
passwd clion
```
4. Give the new user access to the alice subdirs in your usual user's home (replace all $USER occurences) (as root)
```
setacl -m u:clion:rx /home/$USER/alice
```
5. Append the following in /home/clion/.bashrc
```
 source scl_source enable devtoolset-7
 export ALIBUILD_WORK_DIR="/home/$USER/alice/sw"
 WORK_DIR=$ALIBUILD_WORK_DIR
 source /home/$USER/alice/sw/slc7_x86-64/ReadoutCard/latest/etc/profile.d/init.sh #Replace/extend with your package
 source /home/$USER/alice/sw/slc7_x86-64/CMake/latest/etc/profile.d/init.sh
```
6. Follow the instructions from [here](https://www.jetbrains.com/help/clion/remote-projects-support.html) to start a full remote project on CLion running on your local host, with the options outlined below. 

  Toolchain (Addresses on remote host)
  - ssh://clion@$HOSTNAME:22
  - cmake: `/usr/bin/cmake3`
  - make: `/opt/rh/devtoolset-7/root/usr/bin/make`
  - gcc: `/home/$USER/alice/sw/slc7_x86-64/GCC-Toolchain/latest/bin/gcc`
  - g++: `/home/$USER/alice/sw/slc7_x86-64/GCC-Toolchain/latest/bin/g++`
  - gdb: `/home/$USER/alice/sw/slc7_x86-64/GCC-Toolchain/latest/bin/gdb`
  
  CMake
  - Toolchain: the name of the toolchain just created
  - Build options: Add `-j$T` where T = a sensible number of threads for your
    remote system
7. Load CMake Project
8. Build / Run

PS: To use gdb properly, don't forget to pass `-O0` to the `CMAKE_CXX_FLAGS`

### Known issues / quirks:

1. Some times the "Loading cmake project" step might hang. It is unclear why, a restart of the IDE solves the problem.
2. Some times the local and remote files can get out of sync. A change in the remote deployment directory solves it:
   Preferences -> Build, Execution, Deployment -> Deployment. Under the Mappings tab update with a new Deployment Path under /tmp.


Editor
------

Coding guidelines can be applied by using a special settings file. See [here](https://github.com/AliceO2Group/CodingGuidelines#clion).
