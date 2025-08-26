# How Do I Set a Charge Simulation?

| Date       | Category    |
|------------|-------------|
| 2025-08-26 12:47:03 | Charge |


The steps to set up a Charge simulation are very similar to those for an FDTD simulation:

- **Create the geometry**  
  The [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html) object hosts the simulation geometry and enables easy integration with multiphysics.

- **Assign materials**  
  Materials can be defined using [SolidMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SolidMedium.html), which requires specifying heat capacity and thermal conductivity, or [FluidSpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluidSpec.html), which represents a non-simulated fluid.

- **Assign boundary conditions**  
  These can be:
    - [VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html)
    - [CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html)
    - [InsulatingBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.InsulatingBC.html)

- **Add a source**  
  A DC voltage source can be added to the [VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html) using a [DCVoltageSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DCVoltageSource.html) object.  
  Similarly, a [DCCurrentSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DCCurrentSource.html) can be added to the [CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html) boundary to define a current source.

- **Define meshing specifications**  
  The simplest option is to use the [UniformUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.UniformUnstructuredGrid.html) mesh type, where you only need to specify the grid size `dl`. The mesher will automatically generate a mesh that fits the structures while respecting the given resolution.

- **Define the simulation type**  
  Define the simulation type via the `analysis_spec` of the [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html) object. Currently, only [IsothermalSteadyChargeDCAnalysis](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.IsothermalSteadyChargeDCAnalysis.html) is supported.

- **Create the simulation object**  
  Create a [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html) object.

- **Run the simulation**  
  Use `Web.run`, just like with an FDTD simulation.

For a full walkthrough of this process, check out the [HeatSolver example notebook](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver).
