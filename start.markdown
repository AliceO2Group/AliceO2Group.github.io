---
title: Getting Started
layout: main
---

Obtain the code
===============

The ALICE O² Software is hosted on [GitHub](https://github.com) under the
[AliceO2Group](https://github.com/AliceO2Group/) organization. The core package is
[AliceO2](https://github.com/AliceO2Group/AliceO2).

This means you can obtain the source code by cloning the repository:

    git clone https://github.com/AliceO2Group/AliceO2

There is no need for you to clone the repository manually, this part is covered in our
[build instructions](#build).


Build
=====

In order to build the ALICE O² software we use [aliBuild](https://alisw.github.io/alibuild). Check
out our [build instructions](https://alice-doc.github.io/alice-analysis-tutorial/building/).


Run
===

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


Contribute
==========

Since O² uses the Git version control system it is recommended you follow [our AliPhysics Git
tutorial](http://alisw.github.io/git-tutorial/) to learn its rudiments.

Remember to [fork the AliceO2 project on GitHub](https://github.com/AliceO2Group/AliceO2/fork) and
please follow the [coding guidelines](https://github.com/AliceO2Group/CodingGuidelines/), given that
most of them are enforced by automatic checks.


Get support
===========

For simple support questions [please use our Discourse forum](https://alice-talk.web.cern.ch/).

The first time you connect, you will need to hit the **Sign up** button and use your CERN
credentials to register. It is easy to browse existing topics in Discourse, and mark the relevant
reply as a solution. When you create a new discussion topic, Discourse suggests similar topics that
might be duplicates to your issue. Once a topic has been opened from the web interface, every
registered user gets an email notification. It is possible to reply to such emails directly from
your email client if you wish.

If you think you have found a bug in our software, instead of reporting it on the mailing list you
are encouraged to use [JIRA](https://alice.its.cern.ch):

> [Open a ticket on O2 Core and Common Features](https://alice.its.cern.ch/jira/secure/CreateIssue.jspa?pid=11201)

By default the issue type is set to **Bug** and the project is set to **O2 Core and Common
Features**, which is the most used combination, since it mostly concerns the AliceO2 repository. In
case you want to report a different issue type (for instance, you want to suggest a **New feature**)
and your issue concerns a differnt project, please modify the project and the issue type fields
accordingly.
