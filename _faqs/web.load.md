---
title: Web.load?
date: 2025-09-11 18:22:50
enabled: true
category: "Web API"
---
The [`web.load`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.load.html){: .color-primary-hover} function is a convenient utility in Tidy3D that allows you to **download and load simulation results** directly into a [SimulationData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.components.data.sim_data.SimulationData.html){: .color-primary-hover}, [HeatChargeSimulationData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulationData.html){: .color-primary-hover}, or [ModeSolverData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolverData.html){: .color-primary-hover}, depending on the simulation. 

It is particularly useful for retrieving results from simulations created and run through the Tidy3D GUI or API.


## Parameters
- **task_id (str)**: Unique identifier for the simulation task (returned when uploading).
- **path (str)**: Local path where the results file (`.hdf5`) will be saved. Default: `"simulation_data.hdf5"`.
- **replace_existing (bool)**: If `True`, overwrites existing files at the same path.

---

## Example
<div markdown class="code-snippet">
{% highlight python %}
from tidy3d import web

sim_data = web.load(task_id, path="out/sim.hdf5", verbose=True)

# Now you can postprocess or visualize your simulation data
{% endhighlight %}
{% include copy-button.html %}</div>
