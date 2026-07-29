# How Do I Simulate a Bent Anisotropic Waveguide with EME?

| Date       | Category    |
|------------|-------------|
| 2026-04-23 11:26:28 | EME |


# How do I simulate a bent anisotropic waveguide with EME?

Unlike isotropic bends, which can be modeled with a single EME cell (see [how can I simulate bent waveguides with EME](https://www.flexcompute.com/tidy3d/faq/docs/faq/how-can-i-simulate-bent-waveguides-with-eme.html)), anisotropic bends require **multiple EME cells** and a convergence sweep over `num_cells` in [tidy3d.EMEUniformGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEUniformGrid.html).

The reason is that in an anisotropic medium — defined with [tidy3d.FullyAnisotropicMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FullyAnisotropicMedium.html) or [tidy3d.AnisotropicMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.AnisotropicMedium.html) — the permittivity tensor is fixed in the lab frame, but the propagation direction rotates along the arc. The local eigenmodes therefore change continuously, producing polarization mixing and back-reflections. A single EME cell misses this effect and **overestimates transmission**. Dividing the arc into several cells in [tidy3d.EMESimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMESimulation.html) — each with its own curved eigenmode set defined via `bend_radius` in [tidy3d.EMEModeSpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html) — recovers the correct result.





```python
python

mode_spec = td.EMEModeSpec(
    num_modes=num_modes,
    target_neff=target_neff,
    bend_radius=radius,
    bend_axis=1,
)

eme_sim = td.EMESimulation(
    size=(np.pi * radius, plane_size[0], plane_size[1]),  # arc length along propagation axis
    center=(0, 0, 0),
    structures=[waveguide],
    medium=background_medium,
    axis=0,
    freqs=[freq0],
    eme_grid_spec=td.EMEUniformGrid(num_cells=num_cells, mode_spec=mode_spec),
    grid_spec=grid_spec,
    store_coeffs=True,
)
```




For a complete example featuring a 180° LiNbO₃ bend, an FDTD reference simulation, and a cell-count convergence study, refer to [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/AnisotropicBendsEME/).

