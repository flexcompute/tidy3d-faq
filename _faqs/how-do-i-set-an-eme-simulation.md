---
title: How do I set an EME simulation?
date: 2025-05-27 18:52:21
enabled: true
category: "EME"
---
The process of setting up an **EME** simulation is very similar to that of an **FDTD** simulation. The geometry and material specifications are the same. The main difference is the need to define an `eme_grid_spec`, which determines the cells where the eigenmode expansions are computed.

The EME grid can be defined in several ways:
- A **uniformly spaced grid** using the [`tidy3d.EMEUniformGrid`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEUniformGrid.html){: target="_blank" rel="noopener"} object. This is the simplest option and is suitable when the cross-section varies smoothly along the propagation direction. The key parameter is `num_cells`, which controls how many cells the region is divided into.
- A **custom grid** using the [`tidy3d.EMEExplicitGrid`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEExplicitGrid.html){: target="_blank" rel="noopener"} object. Use this when you want full control over cell boundary positions — for example, to place boundaries at junctions, transitions, or other locations where the cross-section changes abruptly.
- A **combination of both** uniform and explicit grids using the [`tidy3d.EMECompositeGrid`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMECompositeGrid.html){: target="_blank" rel="noopener"} object. This is useful for structures that have both uniform and varying sections — for example, a taper connecting two straight waveguides. You can assign a single cell to each uniform section and use a finer grid for the tapered region.

**Tips for choosing the grid:**

- **Uniform sections** (e.g. straight waveguides) only need **one cell** because the cross-section does not change.
- **Varying sections** (e.g. tapers, bends) need enough cells so that each cell is approximately uniform. Use more cells where the cross-section changes rapidly.
- Always perform a **convergence test** by increasing the number of cells and checking that the results (e.g. S-parameters) have stabilized.

Refer to our [EME tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMESolver/){: target="_blank" rel="noopener"} for detailed examples on how to implement the different grid configurations.

