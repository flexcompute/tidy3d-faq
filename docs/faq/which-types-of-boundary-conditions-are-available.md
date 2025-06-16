# Which Types of Boundary Conditions are Available?

| Date       | Category    |
|------------|-------------|
| 2025-06-13 11:47:10 | "Heat" |


There are three different boundary conditions available:

- [TemperatureBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.TemperatureBC.html){: .color-primary-hover}
    This specify a fixed temperature at the boundary surface.

- [HeatFluxBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatFluxBC.html){: .color-primary-hover}:
    This boundary specify heat flux normal to the boundary, which corresponds to the derivative of the temperature normal to the boundary.
    $Q = k\frac{\partial T}{\partial n}$

- [ConvectionBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConvectionBC.html){: .color-primary-hover}:
    Corresponds as convective heat transfer between the domain and the surrounding envrioment
    $-k\frac{\partial T}{\partial n} = h (T-T_\inf)$, where $T_\inf$ is the temperature of the envrioment far from the surface

For more information about the boundary conditions, please refer to our Heat solver [techinical article](https://www.flexcompute.com/tidy3d/learn-center/technical-article/heat-solver-introduction/){: .color-primary-hover}. For an example applicaiton, you can check our [heat tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/HeatSolver/){: .color-primary-hover}.
