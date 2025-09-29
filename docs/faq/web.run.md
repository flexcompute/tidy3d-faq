# Web.run?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 13:50:36 | Web API |


The [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.run.html) function is a high-level API method for submitting a simulation to Flexcompute’s cloud server. It automatically uploads the simulation, runs it remotely, monitors progress, downloads the results, and loads them as a data object.

It is the general method to submit a simulation to the cloud, and it works with the [Simulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html), [HeatChargeSimulation](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.HeatChargeSimulation.html), [web.Batch](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.Batch.html), and [ModeSolver](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolver.html) objects.


## Example


```python
from tidy3d import web

# Submit and run the simulation
sim_data = web.run(
    simulation,
    task_name="my_task",
    path="out/sim.hdf5"
)
```



The `web.run` function requires the `task_name` string.

Optional arguments:

`folder_name`: Where to store the simulation in the web UI (default: "default").

`path`: Local file path to save results (.hdf5).

`verbose`: If True, shows progress (default).
