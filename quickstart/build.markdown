---
title: Build packages
layout: main
---

In order to build our software and manage its internal and external dependencies, we use a tool called `aliBuild` ([repo](https://github.com/alisw/alibuild)). It uses _recipes_ to know how to build each package. The _recipes_ are stored in a dedicated github repository: [alidist](https://github.com/alisw/alidist).

`alienv` is the companion to `aliBuild`. It sets up the environment to be able to run the software. You can either _load_ or _enter_ the environment, depending whether you wish to stay in the same shell or launch a new one. 

Before building the Alice O2 software suite, there are a number of steps to take. They are all described in [this extensive tutorial](https://alice-doc.github.io/alice-analysis-tutorial/building/).

If you just want to run our software, not develop it, please head directly to the section about [binaries](../advanced/binaries.markdown).
