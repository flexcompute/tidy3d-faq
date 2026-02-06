# How can I simulate bent waveguides with EME?

| Date       | Category    |
|------------|-------------|
| 2025-05-27 18:52:22 | EME |


To simulate a **bent waveguide**, it is necessary to define the structure as **straight** in the geometry. The bend is then specified using the `bend_radius` parameter within the [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html) object. In this setup, each EME cell represents a section with the given bend radius, allowing the solver to accurately account for curvature effects. When low losses are expected, it is recommended to use "double" precision in the [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.EMEModeSpec.html) object.

For a detailed example, refer to [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMEBends/).

