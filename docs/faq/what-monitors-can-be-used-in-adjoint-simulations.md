# What Monitors Can Be Used in Adjoint Simulations?

| Date       | Category    |
|------------|-------------|
| 2025-06-19 14:57:18 | Inverse Design |


For adjoint simulations, nearly all frequency-domain monitors can be used to define the objective function:

- [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html)
- [ModeMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeMonitor.html)
- [DiffractionMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DiffractionMonitor.html)

The [FluxMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluxMonitor.html) is currently not supported, but equivalent flux information can be obtained using the [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html), as demonstrated in [this example](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd22PhotonicCrystal/).

We currently don't support field projection monitors, such as [FieldProjectionCartesianMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionCartesianMonitor.html) and [FieldProjectionAngleMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionAngleMonitor.html). For optimizations involving far-field projections, users can use a [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html) to record the near field and locally project it to the far field, as discussed in [this](https://www.flexcompute.com/tidy3d/examples/notebooks/FieldProjections/) tutorial.

Time-domain monitors are also not supported.

We highly recommend watching the [Inverse Design lectures](https://www.flexcompute.com/tidy3d/learning-center/inverse-design/) if you're new to the adjoint method. You can also explore this [tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/) for an introduction to automatic differentiation and adjoint optimization concepts.
