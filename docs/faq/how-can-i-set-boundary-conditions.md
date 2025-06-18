# How Can I Set Boundary Conditions?

| Date       | Category    |
|------------|-------------|
| 2025-06-17 15:50:52 | Heat |


Boundary conditions for heat simulations are defined using the [HeatChargeBoundarySpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeBoundarySpec.html) class, which has two required fields: `condition` and `placement`.

- **`condition`**: Specifies the boundary condition to impose. It accepts one of the following types:
      - [TemperatureBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.TemperatureBC.html)
      - [HeatFluxBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatFluxBC.html)
      - [ConvectionBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConvectionBC.html)

- **`placement`**: Specifies where the boundary condition should be applied. Available options include:

      - [StructureBoundary](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.StructureBoundary.html)
        The boundary of a structure. Only the portion of the boundary not covered by subsequent structures is considered.

      - [StructureStructureInterface](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.StructureStructureInterface.html) 
        The interface between two structures. Specifically, this refers to the boundary of the succeeding structure that lies within the preceding structure.

      - [MediumMediumInterface](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.MediumMediumInterface.html)
        The interface between two media.

      - [SimulationBoundary](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SimulationBoundary.html)
        The boundary of the heat simulation domain. You can specify particular surfaces using the `surfaces` field. By default, all surfaces are selected.

      - [StructureSimulationBoundary](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.StructureSimulationBoundary.html)
        The portion of the heat simulation domain boundary that is covered by a structure. As with `StructureBoundary`, only regions not covered by subsequent structures are included.

You can check out this [HeatSolver](https://www.flexcompute.com/tidy3d/examples/notebooks/HeatSolver/) notebook for an example of how to use it in practice.
