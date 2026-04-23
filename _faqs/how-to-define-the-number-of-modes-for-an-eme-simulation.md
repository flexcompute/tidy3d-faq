---
title: How to define the number of modes for an EME simulation?
date: 2025-05-27 18:52:21
enabled: true
category: "EME"
---
The [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html){: target="_blank" rel="noopener"} object controls how modes are computed in each EME cell. The most important parameters to tune for accuracy and performance are described below.

### `num_modes`

It is important to use a sufficient number of modes to accurately capture the physics of the device and ensure that the simulation results are converged. The exact number of modes required depends on the characteristics of the device. For example, larger waveguides support more propagating modes and therefore require a greater number of modes to achieve accurate results.

A recommended approach is to perform a **convergence sweep**, where the simulation is run with increasing numbers of modes to analyze how the results converge. This can be done efficiently using [`tidy3d.EMEModeSweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSweep.html){: target="_blank" rel="noopener"}, which sweeps over the number of modes without recomputing them. This process is demonstrated at the end of [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMESolver/){: target="_blank" rel="noopener"}.

### `num_pml`

Controls the number of **PML (Perfectly Matched Layer)** layers added at the edges of the mode solving cross-section. Increasing `num_pml` is important when the structure supports **leaky** or **radiative modes** that extend beyond the simulation boundaries. If you observe that results depend on the simulation domain size, adding PML layers can help absorb those radiative components and improve accuracy.

### `sort_spec`

Primarily used in EME for **filtering** and **pinning** modes — for example, to retain only modes of a particular polarization (`te_fraction`), to exclude unwanted higher-order or spurious modes from the expansion, or to pin the mode whose field energy most overlaps a specific region via the `fill_fraction_box` sort key combined with `ModeSortSpec.bounding_box`. The `fill_fraction_box` option is especially useful for multi-waveguide devices (splitters, couplers, directional couplers) where the supermodes of the full cross-section need to be indexed by which waveguide they primarily live in. Filtering the mode set can also improve both accuracy and performance by focusing computational effort on the modes that contribute meaningfully to device behavior.

### `interp_spec`

Controls how modes are **interpolated across frequencies** in broadband simulations. This is set via the `interp_spec` parameter and determines the number of frequency points at which modes are explicitly solved; intermediate frequencies are interpolated. Increasing the number of interpolation points improves broadband accuracy but increases computational cost.

### Other useful parameters

- **`precision`**: Set to `"double"` for simulations that require high accuracy, such as bent waveguides with low expected losses.
- **`bend_radius`** and **`bend_axis`**: Used for simulating **bent waveguides**. The geometry should be defined as straight; the curvature is applied analytically during mode solving. See [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMEBends/){: target="_blank" rel="noopener"} for details.

### Checking convergence

`num_modes` is only one of four discretization choices that interact; in practice all four should be tested together:

- **Number of EME cells** along the propagation axis. EME solves modes at the centre of each cell and treats each cell as translation-invariant, so slowly varying sections (tapers, adiabatic bends, graded transitions) are resolved by splitting them into enough cells for each to be approximately uniform. For such structures the number of cells is typically the first convergence knob — increase `num_cells` on [`tidy3d.EMEUniformGrid`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEUniformGrid.html){: target="_blank" rel="noopener"} (or add boundaries to [`tidy3d.EMEExplicitGrid`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEExplicitGrid.html){: target="_blank" rel="noopener"}) until the S-matrix stops changing.
- **Number of modes per cell** (`num_modes`). [`tidy3d.EMEModeSweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSweep.html){: target="_blank" rel="noopener"} scans this cheaply without re-solving modes.
- **Transverse simulation window plus `num_pml`**. The mode plane must be wide enough that guided modes decay before the edge, and radiation modes have room to resolve.
- **Yee grid resolution** (`grid_spec` on [`tidy3d.EMESimulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMESimulation.html){: target="_blank" rel="noopener"}). Sets the accuracy of the underlying eigenproblem in each cell.

Tighten them one at a time — many "non-converged" symptoms come from under-resolution on a different axis than the one being tuned.

### Diagnostics

**Invalid-mode warnings in the simulation log** usually mean the transverse window or Yee grid is too coarse to support the requested `num_modes`, and the extra modes come back as numerical noise. Widen the simulation and/or refine the grid (and consider more `num_pml`) before lowering `num_modes`. If a physically relevant mode is filtered out because its imaginary effective index is only slightly negative, relax the filter with `increasing_mode_tolerance` on `EMEModeSpec`.

**The S-matrix keeps changing even at large `num_modes`** — add an [`tidy3d.EMECoefficientMonitor`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMECoefficientMonitor.html){: target="_blank" rel="noopener"} to record the forward (`A`) and backward (`B`) amplitudes per cell. If a handful of high-index modes carry significant power in some cell, that cell needs more modes, a finer Yee grid, or a boundary placed at a nearby discontinuity. Set `EMESimulation.store_coeffs=True` to keep the full internal coefficients in `EMESimulationData.coeffs`.

