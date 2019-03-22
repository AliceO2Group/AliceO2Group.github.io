---
title: Coverage Reports
layout: main
---

Introduction
============
Coverage report trends percentage of executed source code during the tests.


g++ flags
=========
Generating coverage data requires specific `g++` flags: `-g -O0 --coverage`, set them only when running coverage tests, for this reason you can use separate `CMAKE_BUILD_TYPE`:

```cmake
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0 --coverage")
endif()
```


Generate reports locally
========================
1. Install `lcov`

2. Run cmake using correct `CMAKE_BUILD_TYPE`, compile code and run tests. This should output `.gcda` files containing coverage data.
3. Use `lcov` to process the reports:
```bash
lcov --directory . --capture --output-file coverage.info
```
4. Remove particular coverage data that does not belong to package itself
```bash
lcov --remove coverage.info '/opt/*' '/usr/*' --output-file coverage.info
```
5. Display coverage report
```bash
lcov --list coverage.info
```

Uploading reports to Codecov from aliBuild
==========================================
...

Uploading reports to Codecov from Travis
========================================
__Disclaimer:__ You can follow these instruction only if you're able to supply all dependencies to the Travis build before it times out.

At first create an account in `codecov`, generate security token: `Account` > `Access` > `Create API token` and provide it to Travis.

Then, follow instruction from previous section, instead of displaying coverage report (Point 5) upload them to codecov:
```yaml
- bash <(curl -s https://codecov.io/bash) || echo "No coverage reports"
```
