---
title: Overview of the ALICE O<sup>2</sup>
layout: main
---

This is an overview of the O<sup>2</sup> system. It is pretty rough, but it should give you an idea of the general architecture. Please refer to other documents such as the [TDR](https://cds.cern.ch/record/2011297).

## Requirements

1. After LS2 the ALICE experiment will have gone through a massive upgrade to handle minimum bias PbPb interactions at 50 kHz. This will results in a 100 times higher event rate than in Run 1 (2010).

2. Moreover, the physics topics addressed by the ALICE upgrade are characterised by a very small signal-to-noise ratio, requiring very large statistics, and a large background, which makes triggering techniques very inefficient, if not impossible.

3. Finally, the inherent rate of  the Time Projection Chamber (TPC) detector is lower than 50kHz, thus requiring a continuous, _non-triggered_, read-out.

## A new computing system: ALICE O<sup>2</sup>

After the upgrade the readout throughput will increase to 3.4TB/s. To store such a data volume is quite challenging. 

This led us to design a new computing system for Run 3 and 4. In this new system the data is compressed on-the-fly by partial online reconstruction, achieving a compression factor of 30. In this unified design, the traditional boundary between online and offline tasks is much thinner. As a consequence, we have a common computing system for online and offline named "O<sup>2</sup>".

## Data flow

The O<sup>2</sup> data flow is depicted below in a simplified way. A more detailed description is available in the [TDR](https://cds.cern.ch/record/2011297).

<img src="{{site.baseurl}}/images/dataflow.png" style="width:85%"/>
