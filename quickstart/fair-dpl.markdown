---
title: FairMQ and DPL
layout: main
---

The Alice O2 components rely on widely used C++ libraries such as Boost and STL. In addition it denepds on in-house libraries:
- _FairMQ_ - transport layer developed by FAIR team, with contributions from ALICE team
- _Data Processing Layer_ (DPL) - abstraction layer developed by ALICE team

## FairMQ 

[FairMQ](https://github.com/FairRootGroup/FairMQ) is part of a framework called [FairRoot](https://github.com/FairRootGroup/FairRoot), developed at GSI. It started as a C++ simulation, reconstruction and analysis framework for the FAIR accelerator. It is now accelerator and experiment agnostic. We use it in ALICE and we contribute back whenever possible. We often refer to the common parts in between FairRoot and O2 as _ALFA_. 

FairMQ provides an asynchronous message passing API to be used in a multi-process topology. Each process is called a __Device__. The underlying __transport__ can be _zeromq_, _shmem_, _nanomsg_, and _ofi_.

In case of problem or questions, we usually create an _issue_ in their GitHub or tag the main developers in our JIRA or Discourse.

## Data Processing Layer (DPL)

The [DPL](https://github.com/AliceO2Group/AliceO2/tree/dev/Framework/Core) is part of AliceO2 and sits on top of FairMQ. We use it on the FLPs and the EPNs, synchronously and asynchronously, for all kind of data processing. In particular, the reconstruction and the data quality control operate within the DPL.

To use it, one has to express the topology programmatically in a _workflow_. Each step of the processing is described as a _DataProcessor_ and is mapped automatically to a FairMQ _Device_. 

See the extensive README [here](https://github.com/AliceO2Group/AliceO2/tree/dev/Framework/Core) for more details.

TODO : goal (shortly), expend on concepts, code example (simple!)
