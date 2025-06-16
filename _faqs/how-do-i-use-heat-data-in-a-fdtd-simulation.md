---
title: How Do I Use Heat Data in a FDTD Simulation?
date: 2025-06-16 16:19:01
enabled: true
category: "Heat"
---
The integration with a Heat and FDTD simulation is seamlessly achieved with the [PerturbationMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PerturbationMedium.html){: .color-primary-hover} and [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html){: .color-primary-hover} objects, which allow the use of the same geometry for both physics simulations. The main steps are:

- Define the [PerturbationMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PerturbationMedium.html){: .color-primary-hover}s and create the [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html){: .color-primary-hover} object.  
- Create the Heat simulation from the [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html){: .color-primary-hover} object using the `from_scene` method.  
- Create the [Simulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html){: .color-primary-hover} object and call the method `Scene.perturbed_mediums_copy`, inputting the temperature information from the Heat simulation data.

The mediums for a Heat simulation are defined using the [PerturbationMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PerturbationMedium.html){: .color-primary-hover} class. This class accepts a `perturbation_spec` object that models the refractive index variation as a function of temperature, such as the [LinearHeatPerturbation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.LinearHeatPerturbation.html){: .color-primary-hover} model, which represents a linear dependence of the refractive index on temperature.

The mediums are then assigned to their respective geometries and included in a [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html){: .color-primary-hover} object. After the Heat simulation is complete, the optical simulation can be easily generated using `Scene.perturbed_mediums_copy`, and `Simulation.from_scene` method, which automatically creates an FDTD simulation object incorporating the temperature data from the Heat simulation.

This process is illustrated in the [Thermally Tuned Ring Resonator](https://www.flexcompute.com/tidy3d/examples/notebooks/ThermallyTunedRingResonator/){: .color-primary-hover} example.

