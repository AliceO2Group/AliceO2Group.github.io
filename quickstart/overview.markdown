---
title: Overview of the ALICE O<sup>2</sup>
layout: main
---

This is an overview of the O<sup>2</sup> system. It is pretty rough, but it should give you an idea of the general architecture. Please refer to other documents such as the [TDR](https://cds.cern.ch/record/2011297).

## Requirements

1. After LS2 the ALICE experiment will have gone through a massive upgrade to handle minimum bias PbPb interactions at 50 kHz. This will results in a 100 times higher event rate than in Run 1 (2010).

2. Moreover, the physics topics addressed by the ALICE upgrade are characterised by a very small signal-to-noise ratio, requiring very large statistics, and a large background, which makes triggering techniques very inefficient, if not impossible.

3. Finally, the TPC's inherent rate of ~50Hz requires a continuous, _non-triggered_, read-out.

## A new computing system: ALICE O<sup>2</sup>

 Given the above requirements, the readout throughput increases to 3.4TB/s. Such amount of data is difficult to store as it was done during Run 1 and 2.

 This lead us to design of a new computing system for Run 3 and 4. In this new system the data is compressed on-the-fly by partial online reconstruction achieving a compression factor of 30. The unified design causes that traditional boundary between online and offline system blurs out. As a consequence, we have a common computing system for online and offline, thus the name "O2".

## Data flow

The data flow is depicted below in a simplified way. A much more detailed description and figure is available in the [TDR](https://cds.cern.ch/record/2011297).

<img src="{{site.baseurl}}/images/dataflow.png" style="width:85%"/>
