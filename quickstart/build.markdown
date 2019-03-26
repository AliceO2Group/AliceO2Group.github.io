---
title: Build packages
layout: main
---

Obtain the code
===============

The ALICE O² Software is hosted on [GitHub](https://github.com) under the
[AliceO2Group](https://github.com/AliceO2Group/) organization. The core package is
[AliceO2](https://github.com/AliceO2Group/AliceO2).

This means you can obtain the source code by cloning the repository:

    git clone https://github.com/AliceO2Group/AliceO2

There is no need for you to clone the repository manually, this part is covered in our
[build instructions](#build).


Build
=====

In order to build the ALICE O² software we use [aliBuild](https://alisw.github.io/alibuild). Check
out our [build instructions](https://alice-doc.github.io/alice-analysis-tutorial/building/) for the
detailed installation procedure. A quick reference follows.

In general, the O2 package can be safely built on CentOS 7 by installing aliBuild and running:

    aliBuild init O2@dev
    aliBuild build O2 --defaults o2

In order to build the entire O2 software stack (including the O2 package and other components) you
can run:

    aliBuild build O2Suite --defaults o2

You should make sure that both the `alidist` and the `O2` directories are up-to-date with upstream
changes: aliBuild will automatically download precompiled binaries on CC7 if those conditions are
met.

In order to build the O2 package and run the tests automatically (as done by the continuous
integration):

    env ALIBUILD_O2_TESTS=1 aliBuild build O2 --defaults o2 --debug

You may want to use the `--debug` option here to have the full output.
