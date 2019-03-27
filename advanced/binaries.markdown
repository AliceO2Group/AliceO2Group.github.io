---
title: Binaries
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


Install the CERN CA
-------------------

Our RPMs are downloaded from HTTPS servers whose certificates are signed by CERN. You need to make
your system recognize the CERN Certification Authority.

Download the certificates, as root (just copy and paste the following two lines, one of them
automatically converts the certificate to the proper format):

```bash
curl https://cafiles.cern.ch/cafiles/certificates/CERN%20Grid%20Certification%20Authority.crt > /etc/pki/ca-trust/source/anchors/cern_grid.pem
curl https://cafiles.cern.ch/cafiles/certificates/CERN%20Root%20Certification%20Authority%202.crt | openssl x509 -inform der -out /etc/pki/ca-trust/source/anchors/cern_root.pem
```

Make them recognized:

```bash
update-ca-trust
```

You can immediately test it:

```bash
curl https://ali-ci.cern.ch
```

If you don't see any HTTPS/SSL error, it means the installation went through.


Configure Yum repository
------------------------

Run, as root:

```bash
cat > /etc/yum.repos.d/alisw-el7.repo <<EOF
[alisw-el7]
name=ALICE Software - EL7
baseurl=https://ali-ci.cern.ch/repo/RPMS/el7.x86_64/
enabled=1
gpgcheck=0
EOF
```

You are all set.


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
