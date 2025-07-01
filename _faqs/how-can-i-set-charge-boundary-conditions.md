---
title: How Can I Set Charge Boundary Conditions?
date: 2025-06-30 21:10:35
enabled: true
category: "Charge"
---
Boundary conditions for heat simulations are defined using the [HeatChargeBoundarySpec](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeBoundarySpec.html){: .color-primary-hover} class, which has two required fields: `condition` and `placement`.

- **`condition`**: Specifies the boundary condition to impose. It accepts one of the following types:

   - [VoltageBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.VoltageBC.html){: .color-primary-hover}
   - [CurrentBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CurrentBC.html){: .color-primary-hover}
   - [InsulatingBC](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.InsulatingBC.html){: .color-primary-hover}

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

You can check out this [Carrier injection based Mach-Zehnder modulator](https://www.flexcompute.com/tidy3d/examples/notebooks/MachZehnderModulator/){: .color-primary-hover} notebook for an example of how to use it in practice.
