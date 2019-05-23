---
title: ALICE O² Software on GitHub
layout: main
---

<img src="{{site.baseurl}}/images/o2logo.png" style="width: 45%; margin: 40px 40px; float: right;"/>

<p style="text-align:justify;">
<b>ALICE (A Large Ion Collider Experiment)</b> is a general purpose, heavy ion collision detector at
the <b>CERN LHC</b>. It is designed to study the physics of strongly interacting matter, and in
particular the properties of <b>Quark-Gluon Plasma (QGP)</b>, using proton-proton, nucleus-nucleus
and proton-nucleus collisions at high energies. The ALICE experiment will be upgraded during the
Long Shutdown&nbsp;2 (LS2, 2020-2021) in order to exploit the full scientific potential of the
future LHC. Such upgrade will pose the challenge the challenge of reading out and inspecting the
Pb–Pb collisions at rates of 50&nbsp;kHz, sampling the pp and p–Pb at up to 200&nbsp;kHz. The
resulting data throughput from the detector has been estimated to be greater than 3.4&nbsp;TB/s for
Pb–Pb events, roughly two orders of magnitude more than in Run&nbsp;2. 
</p>

<p>
To be able to cope with this amount of data, and to be able to store it, we need to compress it intelligently by running the events reconstruction mostly online. The goal is to store 90GB/s, and thus to achieve a compression factor of more than 30. 
</p>

<p style="text-align:justify;">
<b>The O² software framework</b> will provide the necessary abstraction so that common code can
deliver the selected functionality on different platforms. The framework will also support a
concurrent computing model for a wide spectrum of computing facilities, ranging from laptops to the
complete O² system. Off-the-shelf open source software conforming to open standards will be used as
much as possible, either for the development tools or as a basis for the framework itself.
</p>

<p style="text-align:justify;font-style:italic;">
Find the ALICE O² software on GitHub under the
<a href="https://github.com/AliceO2Group">AliceO2Group organisation</a>. Here you can find various
information useful to O² contributors. You might also want to visit our
<a href="http://cern.ch/alice-o2">institutional website</a>.
</p>
<br/>

Local search
============

<script>
  (function() {
    var cx = '011701885831553573830:zsrnqqfrhsg';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:search></gcse:search>
