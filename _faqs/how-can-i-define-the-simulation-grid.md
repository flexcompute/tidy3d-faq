---
title: How Can I Define the Simulation Grid?
date: 2025-08-26 10:06:59
enabled: true
category: "Charge"
---
There are two classes available for defining the grid specification:

- [UniformUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.UniformUnstructuredGrid.html){: .color-primary-hover}:

    - This class implements a simple uniform unstructured grid, with the grid size defined by the `dl` argument. For an application example, see [this](https://www.flexcompute.com/tidy3d/examples/notebooks/MachZehnderModulator/){: .color-primary-hover} example.

 <div markdown class="code-snippet">
{% highlight python %}
heat_grid = UniformUnstructuredGrid(dl=0.1)
{% endhighlight %}
{% include copy-button.html %}</div>

- [DistanceUnstructuredGrid](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DistanceUnstructuredGrid.html){: .color-primary-hover}:

    - This class specifies the mesh size based on the distance from material interfaces. The finer grid near interfaces is defined by the `dl_interface` argument, while the coarser bulk grid size is set using `dl_bulk`. The distances over which `dl_interface` and `dl_bulk` are enforced can be controlled with the `distance_interface` and `distance_bulk` arguments, respectively. For an application example, see [this](https://www.flexcompute.com/tidy3d/examples/notebooks/ThermallyTunedRingResonator/){: .color-primary-hover} example notebook.

 <div markdown class="code-snippet">
{% highlight python %}
heat_grid = DistanceUnstructuredGrid(
     dl_interface=0.1,
     dl_bulk=1,
     distance_interface=0.3,
     distance_bulk=2,
 )
{% endhighlight %}
{% include copy-button.html %}</div>

The user can also add refinement regions to enforce a minimum grid size in a given region using the [GridRefinementRegion](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GridRefinementRegion.html){: .color-primary-hover} object, or along a line using the [GridRefinementLine](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GridRefinementLine.html){: .color-primary-hover} object. An example of this can be found in our [charge solver example](https://www.flexcompute.com/tidy3d/examples/notebooks/ChargeSolver){: .color-primary-hover}.
