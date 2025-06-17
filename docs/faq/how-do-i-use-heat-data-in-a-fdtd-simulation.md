# How Do I Use Heat Data in a FDTD Simulation?

| Date       | Category    |
|------------|-------------|
| 2025-06-17 15:50:52 | Heat |


The integration with a Heat and FDTD simulation is seamlessly achieved with the [PerturbationMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PerturbationMedium.html) and [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html) objects, which allow the use of the same geometry for both physics simulations. The main steps are:  

- Define the [PerturbationMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PerturbationMedium.html)s and create the [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html) object.  
- Create the Heat simulation from the [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html) object using the `from_scene` method.  
- Create the [Simulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html) object and call the method `Scene.perturbed_mediums_copy`, inputting the temperature information from the Heat simulation data.  

The mediums for a Heat simulation are defined using the [PerturbationMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PerturbationMedium.html) class. This class accepts a `perturbation_spec` object that models the refractive index variation as a function of temperature, such as the [LinearHeatPerturbation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.LinearHeatPerturbation.html) model, which represents a linear dependence of the refractive index on temperature.  

The mediums are then assigned to their respective geometries and included in a [Scene](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Scene.html) object. After the Heat simulation is complete, the optical simulation can be easily generated either by using `Scene.perturbed_mediums_copy` in combination with `Simulation.from_scene`, or by using the `Simulation.perturbed_mediums_copy` method, which automatically creates an FDTD simulation object incorporating the temperature data from the Heat simulation.

This process is illustrated in the [Thermally Tuned Ring Resonator](https://www.flexcompute.com/tidy3d/examples/notebooks/ThermallyTunedRingResonator/) example.
