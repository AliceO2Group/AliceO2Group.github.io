---
title: Getting Started
layout: main
---

Get O²
======

The ALICE O² Software is hosted on [GitHub](https://github.com) under the
[AliceO2Group](https://github.com/AliceO2Group/) organization. The core package is
[AliceO2](https://github.com/AliceO2Group/AliceO2).


Build O²
========

In order to build the ALICE O² software we use [aliBuild](https://alisw.github.io/alibuild). Check
out our [build instructions](https://alice-doc.github.io/alice-analysis-tutorial/building/).


Run O²
======

The simplest way to run `AliceO2` is by using directly our nightly builds from CVMFS. If you have a
CERN account, you can connect via SSH to `lxplus7.cern.ch` first to have CVMFS available.

This is how you list all available builds:

    /cvmfs/alice-nightlies.cern.ch/bin/alienv q | grep O2::nightly

And this is how you load one of them:

    /cvmfs/alice-nightlies.cern.ch/bin/alienv enter VO_ALICE@O2::nightly-20171130-1

Nightly builds are also available on selected Grid sites (the ones supporting the
`alice-nightlies.cern.ch` CVMFS repository), allowing for off-CERN testing.

Nightly builds are automatically announced on the <alice-o2-software-support@cern.ch> mailing list.
Read on the [Get support](#get-support) section to know how to subscribe.


Contribute to O²
================

Since O² uses the Git version control system it is recommended you follow [our AliPhysics Git
tutorial](http://alisw.github.io/git-tutorial/) to learn its rudiments.


Get support
===========

For simple support questions (_e.g. I cannot build O2..._) you can use the
<alice-o2-software-support@cern.ch> mailing list.

> [Click here to subscribe to alice-o2-software-support@cern.ch](https://e-groups.cern.ch/e-groups/EgroupsSubscription.do?egroupName=alice-o2-software-support)

**Note:** you need to be a registered ALICE member in order to do that.

You might want to [have a look at the mailing list archive](https://groups.cern.ch/group/alice-o2-software-support)
to avoid posting duplicate questions.

If you have problems subscribing, check with the [ALICE Secretariat](mailto:alice.secretariat@cern.ch)
if you are correctly registered as ALICE member (just send them an email).

If you think you have found a bug in our software, instead of reporting it on the mailing list you
are encouraged to use [JIRA](https://alice.its.cern.ch):

> [Open a ticket on O2 Core and Common Features](https://alice.its.cern.ch/jira/secure/CreateIssue.jspa?pid=11201)

By default the issue type is set to **Bug** and the project is set to **O2 Core and Common
Features**, which is the most used combination, since it mostly concerns the AliceO2 repository. In
case you want to report a different issue type (for instance, you want to suggest a **New feature**)
and your issue concerns a differnt project, please modify the project and the issue type fields
accordingly.
