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
                 alisw-cub+1.8.0-4                      \
                 alisw-alibuild-recipe-tools+0.2.2-1    \
                 alisw-CMake+v3.19.2-5                  \
                 alisw-capstone+4.0.2-20                \
                 alisw-FreeType+v2.10.1-15              \
                 alisw-ms_gsl+2.1.0-2                   \
                 yum install freeglut-devel
```

Then you need to configure a few environment variables:

```bash
export WORK_DIR=/opt/alisw
export ALIBUILD_ARCH_PREFIX=el7
# FIXME: this will need to change according to the release. Use `ls $WORK_DIR/$ALIBUILD_ARCH_PREFIX/O2/` if you don't know the version.
export O2FULLVERSION="v21.01-7"
# FIXME: this is only needed because of an issue in RPM creation
export MS_GSL_ROOT=/opt/alisw/el7/ms_gsl/2.1.0-2/
```

you can then load the build environment with:


```bash
# FIXME: ignore the errors about missing files for now.
. $WORK_DIR/$ALIBUILD_ARCH_PREFIX/O2/$O2FULLVERSION/etc/profile.d/init.sh

# FIXME:  ofi and lz4 have wrong init.sh. This works around the issue.
export LD_LIBRARY_PATH=/opt/alisw/el7/lz4/v1.9.3-6/lib64:/opt/alisw/el7/ofi/v1.7.1-13/lib:$LD_LIBRARY_PATH
```

Assuming that you have cloned your O2 with:

```bash
git config --global http.proxy http://10.161.58.101:8080
git clone https://github.com/AliceO2Group/AliceO2 O2
```

you can then build with:

```bash
mkdir -p O2/objs
cd O2/objs
# FIXME: the parameter can be removed when the problem with macro tests is fixed
cmake -DBUILD_TEST_ROOT_MACROS=OFF ..  
cmake --build . --target all -j40
```

# Developing QC on the FLP  (Experimental)


This is intended for quick tests of the O2 code on the FLP, without having to go through the whole deployment cycle. It's not meant to be a way to deploy software.

*NOTE*: for now this will only work using FLPSuite-0.14.0.

```
# FIXME: this will not be necessary once https://alice.its.cern.ch/jira/browse/O2-1974 is fixed
sudo yum install -y alisw-O2-customization+v1.0.0-2.x86_64 \
                 alisw-RapidJSON+v1.1.0-alice2-3     \
                 alisw-MPFR+v3.1.3-67                   \
                 alisw-googlebenchmark+1.3.0-42         \
                 alisw-defaults-release+v1-11           \
                 alisw-cub+1.8.0-4                      \
                 alisw-alibuild-recipe-tools+0.2.2-1    \
                 alisw-CMake+v3.19.2-5                  \
                 alisw-capstone+4.0.2-20                \
                 alisw-FreeType+v2.10.1-15              \
                 alisw-ms_gsl+2.1.0-2                   \
                 yum install freeglut-devel             \
                 yum install alisw-OpenSSL+v1.0.2o-37   \
                 abseil                                 \
                 MPFR
```

Then you need to configure a few environment variables:

```bash
export WORK_DIR=/opt/alisw
export ALIBUILD_ARCH_PREFIX=el7
# FIXME: this will need to change according to the release. Use `ls $WORK_DIR/$ALIBUILD_ARCH_PREFIX/QualityControl/` if you don't know the version.
export QCFULLVERSION="v1.9.0-1"
# FIXME: this is only needed because of an issue in RPM creation
export MS_GSL_ROOT=/opt/alisw/el7/ms_gsl/2.1.0-2/
```

you can then load the build environment with:


```bash
# FIXME: ignore the errors about missing files for now.
. $WORK_DIR/$ALIBUILD_ARCH_PREFIX/O2/$QCFULLVERSION/etc/profile.d/init.sh

# FIXME:  ofi and lz4 have wrong init.sh. This works around the issue.
export LD_LIBRARY_PATH=/opt/alisw/el7/lz4/v1.9.3-6/lib64:/opt/alisw/el7/ofi/v1.7.1-13/lib:$LD_LIBRARY_PATH
```

Assuming that you have cloned your O2 with:

```bash
git clone https://github.com/AliceO2Group/QualityControl
```

you can then build with:

```bash
mkdir -p O2/objs
cd O2/objs
# FIXME: this is because it will try to do stuff in /usr otherwise
mkdir -p /tmp/qc-install
cmake -DCMAKE_INSTALL_PREFIX=/tmp/qc-install ..
cmake --build . --target all -j40
```