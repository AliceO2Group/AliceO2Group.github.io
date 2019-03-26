---
title: Overview of the ALICE O<sup>2</sup>
layout: main
---

This is an overview of the O2 system. It is pretty rough but it should give you an idea of the general architecture. Please refer to other documents such as the [TDR](https://cds.cern.ch/record/2011297).

## Requirements

1. After LS2 the ALICE experiment will have gone through a massive upgrade and the LHC will deliver to us minimum bias PbPb interactions at 50 kHz, i.e. 
 about a 100 times more data than in 2010.
  
2. Moreover, the physics topics addressed by the ALICE upgrade are characterised by a very small signal-to-noise ratio requiring very large statistics and a large background which makes triggering techniques very inefficient, if not impossible.
  
3. Finally, the TPC has an inherent rate <50Hz requiring to support a continuous, _non-triggered_, read-out. 
  
## A new computing system : ALICE O<sup>2</sup>
  
 For these 3 main reasons, the amount of data to be handled is so large (3.4TB/s) that it is not possible to simply store it as we did during Run 1 and 2. 
 
 This lead us to design a new computing system for Run 3 and 4. In this new system, all interactions are read-out. To handle the very large amount of data, 3.4 TB/s, and store it, we need to compress it intelligently by reconstructing the data online. By doing so, we achieve more than a factor 30 compression and the traditional boundary between online and offline system blurs out. As a consequence, we have a common computing system for online and offline, thus the name “O2”.  
 
## Data Flow

The data flow is depicted below in a very simplified way. The first row of machines is made of __FLPs__ and the second row of __EPNs__. A much more detailed description and figure is available in the [TDR](https://cds.cern.ch/record/2011297). 

<img src="{{site.baseurl}}/images/dataflow.png" style="width:85%"/>