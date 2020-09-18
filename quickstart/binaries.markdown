---
title: Binaries - CVMFS and RPMs
layout: main
---

We provide builds of the O² ecosystem on CVMFS and via RPMs. 

# CVMFS

## On lxplus
You can run our O² CVMFS builds from `lxplus7.cern.ch` to be on the safe side: CVMFS is immediately
available and you can start running in seconds. 

## On your own machine

The following Operating System (OS) is supported:

  * RHEL 7

moreover the following OSes:

* Centos 8
* Ubuntu 18.04 / Debian 7 (and newer)
* macOS Catalina

are supported on a best effort basis for development and analysis needs.

### Setup

CVMFS is available in the form of packages for several operating systems.
[Read the documentation here](https://cernvm.cern.ch/portal/filesystem/quickstart). There is only
one configuration variable to set up after the package is installed. Create the file
`/etc/cvmfs/default.local` and add the following line:

```bash
CVMFS_HTTP_PROXY="DIRECT"
```

There is no need to explicitly configure `CVMFS_REPOSITORIES`.

### Run

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


# RPMs

We currently provide RPMs produced on demand for certain packages. Our RPMs make it possible to
install and run several versions of the same package at the same time. We produce our RPMs for
RHEL 7 or equivalent.

## Yum repositories

There are three RPM repositories available. They are all hosted on EOS as an ordinary CERN
IT-managed website.

The **main repository** contains *non-updatable RPMs* that allow for the installation of multiple versions
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

## Find and install packages

All our packages begin with `alisw`. Search for a package:

```bash
yum search alisw-Control
```

If you don't find the package you want, you may want to try forcing Yum to update its cache:

```bash
yum -v clean expire-cache
```

Install a package:

```bash
yum install -y alisw-Control+v20180613-1
```

All its dependencies will be automatically downloaded. Note that, in the case of non-updatable RPMs, the version number is part of the
actual package name.

## Load packages

You can load packages using the `aliswmod` command. 

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

## Produce RPMs

Use [this Jenkins job](https://alijenkins.cern.ch/job/BuildRPM/) to launch a RPM build. 

## Add external dependencies to RPMs

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

# Automatic builds

Every night (Geneva time) a new O² build is produced and published on `alice-nightlies.cern.ch`. RPMs are produced on-demand
only.

# Develop a single package reusing a CVMFS / RPM installation

*EXPERIMENTAL*

See [here](https://github.com/alice-doc/alice-analysis-tutorial/blob/2df84a5aee5093e72681b6aca465a443bdcfdaed/building/devel.md)

TODO copy paste the instructions here once ready.
