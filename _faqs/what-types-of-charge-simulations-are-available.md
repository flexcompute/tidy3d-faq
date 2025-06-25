---
title: What Types of Charge Simulations are Available?
date: 2025-06-24 19:15:49
enabled: true
category: "Charge"
---
Currently, there are two types of Charge simulations that can be carried out using the [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html){: .color-primary-hover} class:

- **Conduction**:  
    Solves the electrical conduction equation.

- **Charge**:  
    For structures containing a [SemiconductorMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SemiconductorMedium.html){: .color-primary-hover}, the drift-diffusion equations are also solved.

For an application example, please refer to [this](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver/){: .color-primary-hover} example notebook.
