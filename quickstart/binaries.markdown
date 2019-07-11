---
title: Binaries - CVMFS and RPMs
layout: main
---

Automatic builds
================

We provide builds of the O² ecosystem on CVMFS and via installable RPMs. Every night (Geneva time)
a new O² build is produced and published on `alice-nightlies.cern.ch`. RPMs are produced on-demand
instead.


Run from CVMFS
==============

You can run our O² CVMFS builds from `lxplus7.cern.ch` to be on the safe side: CVMFS is immediately
available and you can start running literally in seconds. If you are using your own machine, bear in
mind that the following operating systems should be supported:

  * RHEL 7 (and newer)
  * Ubuntu 16.04/Debian 7 (and newer)

macOS is not supported.


Get CVMFS
---------

CVMFS is available in the form of packages for several operating systems.
[Read the documentation here](https://cernvm.cern.ch/portal/filesystem/quickstart). There is only
one configuration variable to set up after the package is installed. Create the file
`/etc/cvmfs/default.local` and add the following line:

```bash
CVMFS_HTTP_PROXY="DIRECT"
```

There is no need to explicitly configure `CVMFS_REPOSITORIES`.


Run
---

O² is available on `alice-nightlies.cern.ch`. To list the available versions:

```bash
/cvmfs/alice-nightlies.cern.ch/bin/alienv q | grep O2::nightly
```

Note that all CVMFS operations might take a while the first time in case content is not yet
available locally. Subsequent runs will be faster.

To run a specific version do, for instance:

```bash
/cvmfs/alice-nightlies.cern.ch/bin/alienv enter VO_ALICE@O2::nightly-20180614-1
```

A new shell opens with the proper environment set.


Run from RPMs
=============

We currently provide RPMs produced on demand for certain packages. Our RPMs make it possible to
install and run several versions of the same package at the same time. We produce our RPMs for
RHEL 7 or equivalent.


Configure Yum repositories
--------------------------

There are three RPM repositories available. They are all hosted on EOS as an ordinary CERN
IT-managed website.

The **main repository** contains special RPMs that allow for the installation of multiple versions
at the same time. Configure it as follows (as root):

```bash
cat > /etc/yum.repos.d/alisw-el7.repo <<EOF
[alisw-el7]
name=ALICE Software - EL7
baseurl=https://alirepo.web.cern.ch/alirepo/RPMS/el7.x86_64
enabled=1
gpgcheck=0
EOF
```

What is available in the repository can be configured by issuing a pull request to [this
file](https://github.com/alisw/ali-bot/blob/master/publish/aliPublish-rpms.conf).

There are two additional repositories. The **updatable RPMs repository** does not allow for multiple
versions of the same package to be installable at the same time, and it behaves more similarly to
what happens to the system packages. Configure it as follows:

```bash
cat > /etc/yum.repos.d/alisw-upd-el7.repo <<EOF
[alisw-upd-el7]
name=ALICE Software - EL7
baseurl=https://alirepo.web.cern.ch/alirepo/UpdRPMS/el7.x86_64
enabled=1
gpgcheck=0
EOF
```

Open a pull request to [this
file](https://github.com/alisw/ali-bot/blob/master/publish/aliPublish-updatable-rpms.conf) to select
what RPMs are generated.

There is a third repository made of **updatable RPMs for testing purposes**. Configure it as
follows:

```bash
cat > /etc/yum.repos.d/alisw-upd-test-el7.repo <<EOF
[alisw-upd-el7]
name=ALICE Software - EL7
baseurl=https://alirepo.web.cern.ch/alirepo/UpdTestRPMS/el7.x86_64
enabled=1
gpgcheck=0
EOF
```

Open a pull request to [this
file](https://github.com/alisw/ali-bot/blob/master/publish/aliPublish-updatable-test-rpms.conf) to select
what RPMs are generated.


You are all set!


Find and install packages
-------------------------

All our packages begin with `alisw` to prevent confusion. Search a package as usual, for instance:

```bash
yum search alisw-Control
```

If you don't find the package you want, you may want to try forcing Yum to update its cache:

```bash
yum -v clean expire-cache
```

Install a package with, for instance:

```bash
yum install -y alisw-Control+v20180613-1
```

All its dependencies will be automatically downloaded. Note that the version number is part of the
actual package name, allowing for multiple versions of the same package to be installed at the same
time.


Load packages
-------------

You can load packages by means of the `aliswmod` command. This is nothing but a convenience wrapper
around `modulecmd` provided by [environment modules](https://github.com/cea-hpc/modules) with all
the correct paths set.

List all the available packages with:

```bash
aliswmod avail
```

Load a package environment with:

```bash
aliswmod enter Control/v20180613-1
```

You can subsequently exit the new shell that was opened with a simple `exit`.

The command `aliswmod` works the same way as `modulecmd`: if you want, for instance, to load
packages in the current shell without opening a new one with `enter`, you can do:

```bash
eval `aliswmod load Control/v20180613-1`
```

which should work in most Unix shells (including `tcsh`, `ksh`, and `zsh`). Note that, differently
from `modulecmd`, you don't need to specify the shell as it is automatically detected by `aliswmod`
itself.


Produce RPMs
============

The ALICE package publishing mechanism produces RPMs based on certain rules as specified in the
previous section from the cached builds produced by aliBuild on the central repository.

Use [this Jenkins job](https://alijenkins.cern.ch/job/BuildRPM/) to launch a RPM build. This job
will actually launch a "standard" build, but it will wait for the RPM to be created and deployed by
the publisher before exiting.


Add external dependencies to RPMs
---------------------------------

It is possible to add standard system dependencies to the produced RPMs if desired. To do so, it is
sufficient to make the build recipe produce a special file called `.rpm-extra-deps` in the root of
the installation directory. The file should contain the package name and version specification using
the format expected by RPMs.

An example follows: it's similar to the creation of Modulefiles:

```bash
# This is the body of the recipe: add extra RPM dependencies
cat > $INSTALLROOT/.rpm-extra-deps <<EOF
axel >= 2.4
python36 <= 3.7
jq >= 1.5
EOF
```

The file will be created under `$INSTALLROOT` and will be simply ignored by a local installation.
The publisher will create a RPM that installs the given dependencies as well.
