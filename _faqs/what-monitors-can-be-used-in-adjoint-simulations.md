---
title: What Monitors Can Be Used in Adjoint Simulations?
date: 2025-06-19 14:57:18
enabled: true
category: "Inverse Design"
---
For adjoint simulations, nearly all frequency-domain monitors can be used to define the objective function:

- [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html){: .color-primary-hover}
- [ModeMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeMonitor.html){: .color-primary-hover}
- [DiffractionMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DiffractionMonitor.html){: .color-primary-hover}

The [FluxMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluxMonitor.html){: .color-primary-hover} is currently not supported, but equivalent flux information can be obtained using the [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html){: .color-primary-hover}, as demonstrated in [this example](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd22PhotonicCrystal/){: .color-primary-hover}.

We currently don't support field projection monitors, such as [FieldProjectionCartesianMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionCartesianMonitor.html){: .color-primary-hover} and [FieldProjectionAngleMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionAngleMonitor.html){: .color-primary-hover}. For optimizations involving far-field projections, users can use a [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html){: .color-primary-hover} to record the near field and locally project it to the far field, as discussed in [this](https://www.flexcompute.com/tidy3d/examples/notebooks/FieldProjections/){: .color-primary-hover} tutorial.

Time-domain monitors are also not supported.

We highly recommend watching the [Inverse Design lectures](https://www.flexcompute.com/tidy3d/learning-center/inverse-design/){: .color-primary-hover} if you're new to the adjoint method. You can also explore this [tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/){: .color-primary-hover} for an introduction to automatic differentiation and adjoint optimization concepts.
