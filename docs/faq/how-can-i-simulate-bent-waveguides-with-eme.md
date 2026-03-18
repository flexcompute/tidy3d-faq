# How can I simulate bent waveguides with EME?

| Date       | Category    |
|------------|-------------|
| 2025-05-27 18:52:22 | EME |


To simulate a **bent waveguide**, it is necessary to define the structure as **straight** in the geometry. The bend is then specified using the `bend_radius` parameter within the [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html) object. In this setup, each EME cell represents a section with the given bend radius, allowing the solver to accurately account for curvature effects. When low losses are expected, it is recommended to use "double" precision in the [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html) object.

The `EMEModeSpec.bend_medium_frame` field controls how material data in bent cells is interpreted. The default `bend_medium_frame="global"` treats media as fixed in physical space while the bend sweeps through them, matching the global-frame convention used in FDTD. Set `bend_medium_frame="co_rotating"` when the material profile should bend together with the waveguide cross-section, such as a bent fiber or a custom medium sampled directly on the straight EME coordinates. Bent custom media, including `CustomAnisotropicMedium`, are currently only supported for `bend_medium_frame="co_rotating"`.

For isotropic bends, for media whose tensor is effectively invariant under rotation about the bend axis, or when using `bend_medium_frame="co_rotating"`, a single bent EME cell can often represent a long constant-curvature section. For anisotropic bends with `bend_medium_frame="global"`, however, the material orientation seen by the local mode solver generally changes with absolute bend angle. This applies to both `AnisotropicMedium` and reciprocal `FullyAnisotropicMedium`. In that case, a single repeated bent cell may miss longitudinal mode evolution and the associated coupling or back-reflection. For best accuracy, split the bent region into multiple EME cells and check convergence with respect to the number of cells.

For a detailed example, refer to [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMEBends/).
