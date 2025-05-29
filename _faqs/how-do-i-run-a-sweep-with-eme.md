---
title: How do I run a sweep with EME?
date: 2025-05-27 18:52:21
enabled: true
category: "EME"
---
For **length sweeps**, it is convenient to use a [`tidy3d.EMELengthSweep`](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.1/api/_autosummary/tidy3d.EMELengthSweep.html){: target="_blank" rel="noopener"} object, which can be passed to the `sweep_spec` parameter of the [`tidy3d.EMESimulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMESimulation.html){: target="_blank" rel="noopener"} object. This process is demonstrated in [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMESolver/){: target="_blank" rel="noopener"}.

For **frequency sweeps**, it is sufficient to provide a list of frequencies to the `freqs` parameter of the [`tidy3d.EMESimulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMESimulation.html){: target="_blank" rel="noopener"} object.


