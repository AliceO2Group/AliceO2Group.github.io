---
title: Doxygen
layout: main
---

Introduction
============
[Doxygen](http://www.doxygen.nl) is a tool for generating documentation from annotated C++ sources.



Generating Doxygen with CMake
=============================
CMake provides `doxygen_add_docs` function to generate Doxygen configuration file and create make target (`doc`). After running `make doc` the generated files are to moved to `<build>/doc/html`.

Each Doxygen configuration parameter can be overwritten by `set`ing `DOXYGEN_<PARAMETER>` variables in the CMake code.

Fully working, simplified code can be found below:
```cmake
find_package(Doxygen OPTIONAL_COMPONENTS dot)
if (DOXYGEN_FOUND)
  set(DOXYGEN_USE_MDFILE_AS_MAINPAGE "${CMAKE_SOURCE_DIR}/README.md")
  doxygen_add_docs(doc
    ${CMAKE_SOURCE_DIR}
  )
endif(DOXYGEN_FOUND)
```


Deployment to GitHub pages
==========================
Travis can easily deploy the documentation to the GitHub pages, but it requires GitHub access token. In order to generate one go to `Your profile` > `Settings` > `Developer settings` > `Personal access tokens`, and make sure `public_repo` scope is checked. Afterwards provide the token to Travis by setting it in Travis job settings (`More options` > `Settings`), name it `GITHUB_API_TOKEN`.

Add `linux` build to your build matrix and make sure following packages are present: `cmake`, `doxygen`, `doxygen-doc`, `doxygen-latex`, `doxygen-gui`, `graphviz`. In the `script` section of the travis configuration you need to run `cmake` and `make doc`.

The sample Travis build matrix can be found below:
```
- os: linux
  if: branch = master
  dist: xenial
  env: TOOL=docs
  addons:
    apt:
      sources:
        - ubuntu-toolchain-r-test
      packages:
        - cmake
        - doxygen
        - doxygen-doc
        - doxygen-latex
        - doxygen-gui
        - graphviz
  deploy:
    provider: pages
    skip_cleanup: true
    github_token: $GITHUB_API_TOKEN
    local_dir: build/doc/html
```

Eventually in your GH repo `Settings` scroll down to `GitHub Pages` and set source to `gh-pages` branch.

References
==========
1. [CMake with complete doxygen configuration](https://github.com/AliceO2Group/Monitoring/blob/dev/doc/CMakeLists.txt)
2. [Travis configuration file](https://github.com/AliceO2Group/Monitoring/blob/dev/.travis.yml)
3. [Official travis docs on deployments](https://docs.travis-ci.com/user/deployment/pages/)
