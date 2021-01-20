---
title: Build packages
layout: main
---

In order to build our software and manage its internal and external dependencies, we use a tool called `aliBuild` ([repo](https://github.com/alisw/alibuild)). It uses _recipes_ to know how to build each package. The _recipes_ are stored in a dedicated github repository: [alidist](https://github.com/alisw/alidist).

`alienv` is the companion to `aliBuild`. It sets up the environment to be able to run the software. You can either _load_ or _enter_ the environment, depending whether you wish to stay in the same shell or launch a new one. 

To build our software, please follow carefully [this extensive tutorial](https://alice-doc.github.io/alice-analysis-tutorial/building/).

If you just want to run our software, not develop it, please head directly to the section about [binaries](binaries.markdown).

# Developing O2 on the FLP  (Experimental)

This is intended for quick tests of the O2 code on the FLP, without having to go through the whole deployment cycle. It's not meant to be a way to deploy software.

*NOTE*: for now this will only work using FLPSuite-0.14.0.

```
# FIXME: this will not be necessary once https://alice.its.cern.ch/jira/browse/O2-1974 is fixed
sudo yum install -y alisw-O2-customization+v1.0.0-2.x86_64 \
                 alisw-RapidJSON+v1.1.0-alice2-3     \
                 alisw-MPFR+v3.1.3-67                   \
                 alisw-googlebenchmark+1.3.0-42         \
                 alisw-defaults-release+v1-11           \
                 alisw-MPFR+v3.1.3-67                   \
                 alisw-cub+1.8.0-4                      \
                 alisw-alibuild-recipe-tools+0.2.2-1    \
                 alisw-CMake+v3.19.2-5                  \
                 alisw-capstone+4.0.2-20                \
                 alisw-FreeType+v2.10.1-15              \
                 alisw-ms_gsl+2.1.0-2
```

Then you need to configure a few environment variables:

```bash
export WORK_DIR=/opt/alisw
export ALIBUILD_ARCH_PREFIX=el7
# FIXME: this will need to change according to the release.
export O2_VERSION="v21.01-7"
# FIXME: this is only needed because of an issue in RPM creation
export MS_GSL_ROOT=/opt/alisw/el7/ms_gsl/2.1.0-2/
```

you can then load the build environment with:


```bash
# FIXME: ignore the errors about missing files for now.
. $WORK_DIR/$ALIBUILD_ARCH_PREFIX/O2/$O2_VERSION/etc/profile.d/init.sh

# FIXME: needed because of an issue with O2 CMake detection of FairMQ deps
export LD_LIBRARY_PAYH=/opt/alisw/el7/ofi/v1.7.1-13/lib:$LD_LIBRARY_PATH
```

Assuming that you have cloned your O2 with:

```bash
git config --global http.proxy http://10.161.58.101:8080
git clone https://github.com/AliceO2Group/AliceO2 O2
```

you can then build with:

```bash
mkdir O2/objs
cd O2/objs
# FIXME: required because libofi is not exposed as a dependency.
cmake .. -DBUILD_TEST_ROOT_MACROS=OFF -DOFI_ROOT=/opt/alisw/el7/ofi/v1.7.1-13 -DCMAKE_EXE_LINKER_FLAGS="-Wl,--unresolved-symbols=ignore-all"
# FIXME: preload needed because apparently asiofi uses RUNPATH see https://github.com/FairRootGroup/asiofi/issues/7
LD_PRELOAD=/opt/alisw/el7/ofi/v1.7.1-13/lib/libfabric.so.1 cmake --build . --target all -j40
```
