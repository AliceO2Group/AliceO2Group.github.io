---
title: Getting O2
layout: main
---

# Running from CVMFS

If you simply want to run AliceO2 on a Centos6 / Centos7 system e.g. on
lxplus, the simplest way to get a running environment is to use the nightly
builds which get deployed every day in the `/cvmfs/alice-nightlies.cern.ch/`
repository.

Available builds can be listed from lxplus with something like:

    /cvmfs/alice-nightlies.cern.ch/bin/alienv q | grep O2::nightly

You can use the builds with:

    /cvmfs/alice-nightlies.cern.ch/bin/alienv enter VO_ALICE@O2::nightly-20171130-1

Those builds can be used on selected Grid sites supporting
alice-nightlies.cern.ch too, which will be useful for off-site testing (I have
analysis facilities in mind, for instance).

Announcements for new O2 builds will be automatically done on the
alice-o2-software-support@cern.ch mailing list. They will contain also the
exact copy-paste command to issue on lxplus/lxplus7 for using them.
