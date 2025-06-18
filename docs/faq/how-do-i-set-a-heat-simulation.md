# How Do I Set a Heat Simulation?

| Date       | Category    |
|------------|-------------|
| 2025-06-17 15:50:52 | Heat |


The steps to set up a heat simulation are very similar to those for an FDTD simulation:

- **Create the geometry**  
  The [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html) object hosts the simulation geometry and enables easy integration with multiphysics.

- **Assign materials**  
  Materials can be defined using [SolidMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SolidMedium.html), which requires specifying heat capacity and thermal conductivity, or [FluidSpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluidSpec.html), which represents a non-simulated fluid.

- **Assign boundary conditions**  
  These can be:
    - [TemperatureBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.TemperatureBC.html)
    - [ConvectionBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConvectionBC.html)
    - [HeatFluxBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatFluxBC.html)

- **Add a heat source**  
  Use the [HeatSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatSource.html) object to define a volume heating source.

- **Define meshing specifications**  
  The simplest option is to use the [UniformUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.UniformUnstructuredGrid.html) mesh type, where you only need to specify the grid size `dl`. The mesher will automatically generate a mesh that fits the structures while respecting the given resolution. For more information about meshing options, please refer to our technical article [heat-solver-introduction](https://www.flexcompute.com/tidy3d/learn-center/technical-article/heat-solver-introduction/).

- **Create the simulation object**  
  Create a [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html) object.

- **Run the simulation**  
  Use `Web.run`, just like with an FDTD simulation.

For a full walkthrough of this process, check out the [HeatSolver example notebook](https://www.flexcompute.com/tidy3d/examples/notebooks/HeatSolver/).
