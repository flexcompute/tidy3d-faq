---
title: Web.run?
date: 2025-09-16 13:50:36
enabled: true
category: "Web API"
---
The [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.run.html){: .color-primary-hover} function is a high-level API method for submitting a simulation to Flexcompute’s cloud server. It automatically uploads the simulation, runs it remotely, monitors progress, downloads the results, and loads them as a data object.

It is the general method to submit a simulation to the cloud, and it works with the [Simulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html){: .color-primary-hover}, [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html){: .color-primary-hover}, [web.Batch](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.Batch.html){: .color-primary-hover}, and [ModeSolver](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolver.html){: .color-primary-hover} objects.


## Example
<div markdown class="code-snippet">
{% highlight python %}
from tidy3d import web

# Submit and run the simulation
sim_data = web.run(
    simulation,
    task_name="my_task",
    path="out/sim.hdf5"
)
{% endhighlight %}
{% include copy-button.html %}</div>

The `web.run` function requires the `task_name` string.

Optional arguments:

`folder_name`: Where to store the simulation in the web UI (default: "default").

`path`: Local file path to save results (.hdf5).

`verbose`: If True, shows progress (default).
