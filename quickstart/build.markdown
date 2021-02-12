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
sudo yum install -y alisw-CMake+v3.19.2-5  \
                    alisw-FreeType+v2.10.1-15  \
                    alisw-GMP+v6.0.0-62  \
                    alisw-MPFR+v3.1.3-74  \
                    alisw-O2-customization+v1.0.0-2  \
                    alisw-Python-modules-list+1.0-23  \
                    alisw-RapidJSON+v1.1.0-alice2-3  \
                    alisw-alibuild-recipe-tools+0.2.2-1  \
                    alisw-autotools+v1.6.3-9  \
                    alisw-bz2+1.0.8-14  \
                    alisw-capstone+4.0.2-20  \
                    alisw-defaults-release+v1-11  \
                    alisw-double-conversion+v3.1.5-34  \
                    alisw-flatbuffers+v1.11.0-38  \
                    alisw-googlebenchmark+1.3.0-42  \
                    alisw-googletest+1.8.0-48  \
                    alisw-libffi+v3.2.1-21  \
                    alisw-ms_gsl+2.1.0-2  \
                    alisw-re2+2019-09-01-34  \
                    alisw-sqlite+v3.15.0-22
```

Then you need to configure a few environment variables:

```bash
export WORK_DIR=/opt/alisw
export ALIBUILD_ARCH_PREFIX=el7
# FIXME: this will need to change according to the release.
export O2FULLVERSION="v21.05-1"
# Fixed upstream. This is only needed because ms_gsl was not bumped.
export MS_GSL_ROOT=/opt/alisw/el7/ms_gsl/2.1.0-2/
```

you can then load the build environment with:


```bash
# Ignore the errors about missing files for now. Fixed upstream.
. $WORK_DIR/$ALIBUILD_ARCH_PREFIX/O2/$O2FULLVERSION/etc/profile.d/init.sh
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
cmake .. 
cmake --build . --target all -j40
```
