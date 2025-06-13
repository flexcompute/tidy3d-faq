---
title: How Can I Set Boundary Conditions?
date: 2025-06-13 19:29:15
enabled: true
category: "Heat"
---
Boundary conditions for heat simulations are defined using the [HeatBoundarySpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatBoundarySpec.html){: .color-primary-hover} class, which has two required fields: `condition` and `placement`.

- **`condition`**: Specifies the boundary condition to impose. It accepts one of the following types:
      - [TemperatureBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.TemperatureBC.html#tidy3d.TemperatureBC){: .color-primary-hover}
      - [HeatFluxBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatFluxBC.html#tidy3d.HeatFluxBC){: .color-primary-hover}
      - [ConvectionBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ConvectionBC.html#tidy3d.ConvectionBC){: .color-primary-hover}

- **`placement`**: Specifies where the boundary condition should be applied. Available options include:

      - [StructureBoundary](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.StructureBoundary.html){: .color-primary-hover}
        The boundary of a structure. Only the portion of the boundary not covered by subsequent structures is considered.

      - [StructureStructureInterface](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.StructureStructureInterface.html){: .color-primary-hover} 
        The interface between two structures. Specifically, this refers to the boundary of the succeeding structure that lies within the preceding structure.

      - [MediumMediumInterface](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.MediumMediumInterface.html){: .color-primary-hover}
        The interface between two media.

      - [SimulationBoundary](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SimulationBoundary.html){: .color-primary-hover}
        The boundary of the heat simulation domain. You can specify particular surfaces using the `surfaces` field. By default, all surfaces are selected.

      - [StructureSimulationBoundary](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.StructureSimulationBoundary.html){: .color-primary-hover}
        The portion of the heat simulation domain boundary that is covered by a structure. As with `StructureBoundary`, only regions not covered by subsequent structures are included.

You can check out this [HeatSolver](https://www.flexcompute.com/tidy3d/examples/notebooks/HeatSolver/){: .color-primary-hover} notebook for an example of how to use it in practice.
