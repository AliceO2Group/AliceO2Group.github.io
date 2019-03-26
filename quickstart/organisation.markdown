---
title: Code organisation
layout: main
---

<link type="text/css" rel="stylesheet" href="../main.css" />

All the ALICE O<sup>2</sup> code is stored in the [__AliceO2Group__](https://github.com/AliceO2Group) GitHub group.  It is divided into 10 repositories, ranging from the pretty large, like `AliceO2`, to smaller common modules, such as Monitoring or QualityControl. We try to stay on the thin line between 1 huge monolithic repository and a multitude of tiny inter-coupled repositories.

The detector specific code usually goes to AliceO2 (simulation, reconstruction and calibration) or to QualityControl.

Here is the list of our software repositories :

1. [AliceO2](https://github.com/AliceO2Group/AliceO2)<br/>
The ALICE O2 software repository contains the framework, as well as the detector specific, code for the reconstruction, calibration and simulation for the ALICE experiment at CERN for Run 3 and 4. It also encompasses the commonalities such as the data format, and the global algorithms like the global tracking. <br/>
The code organization of this specific repository is explained [here](https://github.com/AliceO2Group/AliceO2/blob/dev/doc/CodeOrganization.md).
1. [AliTPCCommon](https://github.com/AliceO2Group/AliTPCCommon)
1. [Control](https://github.com/AliceO2Group/Control)
1. [Configuration](https://github.com/AliceO2Group/Configuration)
1. [DataDistribution](https://github.com/AliceO2Group/DataDistribution)
1. [InfoLogger](https://github.com/AliceO2Group/InfoLogger)
1. [QualityControl](https://github.com/AliceO2Group/QualityControl)<br/>
Framework and infrastructure for all aspects related to the quality of the data (traditionally called online Data Quality Monitoring, DQM, and offline Quality Assurance, QA).
1. [Readout](https://github.com/AliceO2Group/Readout)
1. [ReadoutCard](https://github.com/AliceO2Group/ReadoutCard)
1. [WebUi](https://github.com/AliceO2Group/WebUi)
