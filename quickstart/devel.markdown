---
title: Development process
layout: main
---

Once your aliBuild setup is complete it is not necessary to run `aliBuild` command each time the code is modified. The development process looks like this (using AliceO2 as an example):
1. Load environment: `alienv load O2/latest`
2. Modify some code
3. Go to the build directory: `cd sw/BUILD/O2-latest/O2`
4. Rebuild: `cmake --build . --target install`
5. Once you are happy with your changes, create a Pull Request (see the section below)

Of course the same process works with any other repository, e.g. QualityControl or Readout.

To develop on top of a CVFMS or RPMs installation, see [here](binaries.markdown).

Contribute
==========

Since O² uses the Git version control system it is recommended you follow [our AliPhysics Git
tutorial](http://alisw.github.io/git-tutorial/) to learn its rudiments.

Remember to [fork the AliceO2 project on GitHub](https://github.com/AliceO2Group/AliceO2/fork) and
please follow the [coding guidelines](https://github.com/AliceO2Group/CodingGuidelines/), given that
most of them are enforced by automatic checks.

Pull request flow
=================

Once you have some code change ready, you can open a pull request (PR) to the relevant AliceO2 repository. If you are a member of the AliceO2Group organization or a long time contributor to it, your pull request will be automatically tested. If you are a first time contributor, you will have to wait for someone to review and approve your PR.

Draft (WIP) Pull requests
-------------------------

In case you are not ready for a PR to be reviewed, you can [mark it as "Draft"](https://github.blog/2019-02-14-introducing-draft-pull-requests/). This will prevent notifying the reviewers and running the tests.

*DEPRECATED*: You can also start the PR title with either `WIP` or `[WIP]` and it will have the same effect. Notice this is deprecated and will be removed at some point in the future.

Run the tests the same way as the CI
---
When a test is failing in a PR it can be useful to run it ourselves in a similar environment. One needs to install docker first. 

1. `docker pull alisw/slc7-builder` # or you can also fetch another builder obviously, but slc7-builder is convenient since there are precompiled binaries so it is fast. It is the one used for build/O2/alidist
2. `docker run -ti alisw/slc7-builder /bin/bash`
3. `pip install alibuild`
4. `aliBuild init O2@dev`
5. `aliBuild --defaults o2 init whateverpackage@whateveryoulike`
6. `ALIBUILD_O2_TESTS=1 aliBuild --defaults o2 build whateverpackage --debug`

