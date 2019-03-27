---
title: Development process
layout: main
---

Once the build machine is setup it is not necessary to run alibuild each time code is modified. The development process looks like 
1. Load environment : `alienv load O2/latest`
2. Modify some code, for example in AliceO2
3. Go to the build directory : `cd sw/BUILD/O2-latest/O2`
4. Rebuild : `make -j install`
5. Once you are happy with your changes, create a Pull Request (see the section below)

Of course the same process works with any repository, e.g. QualityControl or Readout.

Contribute
==========

Since O² uses the Git version control system it is recommended you follow [our AliPhysics Git
tutorial](http://alisw.github.io/git-tutorial/) to learn its rudiments.

Remember to [fork the AliceO2 project on GitHub](https://github.com/AliceO2Group/AliceO2/fork) and
please follow the [coding guidelines](https://github.com/AliceO2Group/CodingGuidelines/), given that
most of them are enforced by automatic checks.