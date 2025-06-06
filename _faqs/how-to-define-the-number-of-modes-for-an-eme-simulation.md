---
title: How to define the number of modes for an EME simulation?
date: 2025-05-27 18:52:21
enabled: true
category: "EME"
---
It is important to use a sufficient number of modes to accurately capture the physics of the device and ensure that the simulation results are converged. The exact number of modes required depends on the characteristics of the device. For example, larger waveguides support more propagating modes and therefore require a greater number of modes to achieve accurate results.

A recommended approach is to perform a **convergence sweep**, where the simulation is run with increasing numbers of modes to analyze how the results converge. This process is demonstrated at the end of [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMESolver/){: target="_blank" rel="noopener"}.


