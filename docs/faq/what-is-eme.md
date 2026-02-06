# What is EME?

| Date       | Category    |
|------------|-------------|
| 2025-05-27 18:52:21 | EME |


The **EigenMode Expansion (EME)** method is a frequency-domain technique useful for simulating very long waveguide-based structures. Its main advantage is that uniform sections of the structure require only a single cell for computation, while varying sections can be efficiently approximated using a limited number of cells. This approach can significantly reduce computational costs compared to FDTD method, while delivering highly comparable results.

Key capabilities of the Tidy3D EME solver include:

- **Bidirectional propagation** — Computes the full bidirectional scattering matrix, accounting for reflections and backward-propagating modes at every interface.
- **Passivity and unitarity constraints** — Optional constraints ensure physically meaningful scattering matrices at cell interfaces (see the `constraint` parameter of [`tidy3d.EMESimulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMESimulation.html)).
- **Bent waveguides** — Simulates curved structures via `bend_radius` in [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html).
- **Anisotropic materials** — Supports diagonally anisotropic media (`tidy3d.AnisotropicMedium`).
- **Fast parameter sweeps** — Efficiently sweeps cell lengths, number of modes, and number of periodic repetitions without recomputing modes (see [`tidy3d.EMELengthSweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMELengthSweep.html), [`tidy3d.EMEModeSweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSweep.html), [`tidy3d.EMEPeriodicitySweep`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEPeriodicitySweep.html)).
- **Broadband frequency interpolation** — Modes are interpolated across frequencies to reduce cost (see `interp_spec` in [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html)).
- **Diagnostics** — Access mode coefficients, interface S matrices, overlaps, and propagation indices via [`tidy3d.EMECoefficientMonitor`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMECoefficientMonitor.html).

Some common application examples include [MMIs](https://www.flexcompute.com/tidy3d/examples/notebooks/MultiplexingMMI/), [tapers and couplers](https://www.flexcompute.com/tidy3d/examples/notebooks/EMESolver/), and [bent waveguides](https://www.flexcompute.com/tidy3d/examples/notebooks/EMEBends/).


