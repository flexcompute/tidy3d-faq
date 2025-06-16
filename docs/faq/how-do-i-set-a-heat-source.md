# How Do I Set a Heat Source?

| Date       | Category    |
|------------|-------------|
| 2025-06-16 16:19:01 | "Heat" |


The heat source is defined using the [HeatSource](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatSource.html){: .color-primary-hover} object. Users can specify the volumetric heating rate, which can be uniform, or spatially varying using a [SpatialDataArray](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SpatialDataArray.html){: .color-primary-hover} object. The source can be applied to any structure within the simulation domain.


In practice, one often wants to model a heater with external current applied. To model this Joule heat source, we can calculate the volumetric Joule heat generation using

$$\frac{dP}{dV} = \frac{1}{\sigma}(\frac{I}{w_{heater}h_{heater}})^2$$

where $\sigma$ is the electrical conductivity of the heater material, I is the applied current, $w_{heater}$ and $h_{heater}$ are the width and thickness of the heater, respectively.

For more information, please check our Heat solver techinical [article](https://www.flexcompute.com/tidy3d/learn-center/technical-article/heat-solver-introduction/){: .color-primary-hover}.
