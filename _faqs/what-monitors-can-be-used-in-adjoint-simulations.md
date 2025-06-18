---
title: What Monitors Can Be Used in Adjoint Simulations?
date: 2025-06-18 13:37:32
enabled: true
category: "Inverse Design"
---
For adjoint simulations, nearly all frequency-domain monitors can be used to define the objective function:

- [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html){: .color-primary-hover}
- [ModeMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeMonitor.html){: .color-primary-hover}
- [DirectivityMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DirectivityMonitor.html){: .color-primary-hover}
- [FieldProjectionCartesianMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionCartesianMonitor.html){: .color-primary-hover}
- [FieldProjectionAngleMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldProjectionAngleMonitor.html){: .color-primary-hover}

The [FluxMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluxMonitor.html){: .color-primary-hover} is currently not supported, but equivalent flux information can be obtained using the [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html){: .color-primary-hover}, as demonstrated in [this example](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd22PhotonicCrystal/){: .color-primary-hover}.

Time-domain monitors are not supported.

We highly recommend watching the [Inverse Design lectures](https://www.flexcompute.com/tidy3d/learning-center/inverse-design/){: .color-primary-hover} if you're new to the adjoint method. You can also explore this [tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/){: .color-primary-hover} for an introduction to automatic differentiation and adjoint optimization concepts.
