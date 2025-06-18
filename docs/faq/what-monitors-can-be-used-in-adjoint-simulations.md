# What Monitors Can Be Used in Adjoint Simulations?

| Date       | Category    |
|------------|-------------|
| 2025-06-18 13:37:32 | Inverse Design |


For adjoint simulations, nearly all frequency-domain monitors can be used to define the objective function:

- [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html)
- [ModeMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeMonitor.html)
- [DirectivityMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DirectivityMonitor.html)
- [FieldProjectionCartesianMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionCartesianMonitor.html)
- [FieldProjectionAngleMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionAngleMonitor.html)

The [FluxMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluxMonitor.html) is currently not supported, but equivalent flux information can be obtained using the [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html), as demonstrated in [this example](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd22PhotonicCrystal/).

Time-domain monitors are not supported.

We highly recommend watching the [Inverse Design lectures](https://www.flexcompute.com/tidy3d/learning-center/inverse-design/) if you're new to the adjoint method. You can also explore this [tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/) for an introduction to automatic differentiation and adjoint optimization concepts.
