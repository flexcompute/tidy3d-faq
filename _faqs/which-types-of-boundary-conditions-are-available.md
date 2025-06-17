---  
title: Which Types of Boundary Conditions are Available?  
date: 2025-06-13 11:47:10  
enabled: true  
category: "Heat"  
---

There are three different boundary conditions available:  

- [TemperatureBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.TemperatureBC.html){: .color-primary-hover}:  
  This specifies a fixed temperature at the boundary surface.  

- [HeatFluxBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatFluxBC.html){: .color-primary-hover}:  
  This boundary specifies heat flux normal to the boundary, which corresponds to the derivative of the temperature normal to the boundary.  
  $Q = k\frac{\partial T}{\partial n}$  

- [ConvectionBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConvectionBC.html){: .color-primary-hover}:  
  This corresponds to convective heat transfer between the domain and the surrounding environment.  
  $-k\frac{\partial T}{\partial n} = h (T - T_\infty)$, where $T_\infty$ is the temperature of the environment far from the surface.  

For more information about the boundary conditions, please refer to our Heat solver [technical article](https://www.flexcompute.com/tidy3d/learn-center/technical-article/heat-solver-introduction/){: .color-primary-hover}. For an example application, you can check our [heat tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/HeatSolver/){: .color-primary-hover}.
