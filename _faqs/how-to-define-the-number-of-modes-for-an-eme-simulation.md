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

Primarily used in EME for **filtering** modes — for example, to retain only modes of a particular polarization or to exclude unwanted higher-order or spurious modes from the expansion. Filtering the mode set can improve both accuracy and performance by focusing computational effort on the modes that contribute meaningfully to device behavior.

### `interp_spec`

Controls how modes are **interpolated across frequencies** in broadband simulations. This is set via the `interp_spec` parameter and determines the number of frequency points at which modes are explicitly solved; intermediate frequencies are interpolated. Increasing the number of interpolation points improves broadband accuracy but increases computational cost.

### Other useful parameters

- **`precision`**: Set to `"double"` for simulations that require high accuracy, such as bent waveguides with low expected losses.
- **`bend_radius`** and **`bend_axis`**: Used for simulating **bent waveguides**. The geometry should be defined as straight; the curvature is applied analytically during mode solving. See [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMEBends/){: target="_blank" rel="noopener"} for details.

