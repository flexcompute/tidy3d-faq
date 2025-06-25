---
title: How Do I Set a Charge Simulation?
date: 2025-06-24 19:15:49
enabled: true
category: "Charge"
---
The steps to set up a Charge simulation are very similar to those for an FDTD simulation:

- **Create the geometry**  
  The [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html){: .color-primary-hover} object hosts the simulation geometry and enables easy integration with multiphysics.

- **Assign materials**  
  Materials can be defined using [SolidMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SolidMedium.html){: .color-primary-hover}, which requires specifying heat capacity and thermal conductivity, or [FluidSpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluidSpec.html){: .color-primary-hover}, which represents a non-simulated fluid.

- **Assign boundary conditions**  
  These can be:
    - [VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html){: .color-primary-hover}
    - [CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html){: .color-primary-hover}
    - [InsulatingBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.InsulatingBC.html){: .color-primary-hover}

- **Add a source**  
  A DC voltage source can be added to the [VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html){: .color-primary-hover} using a [DCVoltageSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DCVoltageSource.html){: .color-primary-hover} object.  
  Similarly, a [DCCurrentSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DCCurrentSource.html){: .color-primary-hover} can be added to the [CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html){: .color-primary-hover} boundary to define a current source.

- **Define meshing specifications**  
  The simplest option is to use the [UniformUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.UniformUnstructuredGrid.html){: .color-primary-hover} mesh type, where you only need to specify the grid size `dl`. The mesher will automatically generate a mesh that fits the structures while respecting the given resolution.

- **Create the simulation object**  
  Create a [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html){: .color-primary-hover} object.

- **Run the simulation**  
  Use `Web.run`, just like with an FDTD simulation.

For a full walkthrough of this process, check out the [HeatSolver example notebook](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver){: .color-primary-hover}.
