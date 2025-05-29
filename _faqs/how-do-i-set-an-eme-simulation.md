---
title: How do I set an EME simulation?
date: 2025-05-27 18:52:21
enabled: true
category: "EME"
---
The process of setting up an **EME** simulation is very similar to that of an **FDTD** simulation. The geometry and material specifications are the same. The main difference is the need to define an `eme_grid_spec`, which determines the cells where the eigenmode expansions are computed.

The EME grid can be defined in several ways:
- A **uniformly spaced grid** using the [`tidy3d.EMEUniformGrid`](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.0/api/_autosummary/tidy3d.EMEUniformGrid.html#tidy3d.EMEUniformGrid){: target="_blank" rel="noopener"} object.
- A **custom grid** using the [`tidy3d.EMEExplicitGrid`](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.0/api/_autosummary/tidy3d.EMEExplicitGrid.html#tidy3d.EMEExplicitGrid){: target="_blank" rel="noopener"} object.
- A **combination of both** uniform and explicit grids using the [`tidy3d.EMECompositeGrid`](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.0/api/_autosummary/tidy3d.EMECompositeGrid.html#tidy3d.EMECompositeGrid){: target="_blank" rel="noopener"} object.

Refer to our [EME tutorial](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.0/api/_autosummary/tidy3d.EMEUniformGrid.html#tidy3d.EMEUniformGrid){: target="_blank" rel="noopener"} for detailed examples on how to implement the different grid configurations.

