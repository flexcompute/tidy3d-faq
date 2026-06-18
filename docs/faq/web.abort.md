# Web.abort?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 13:50:36 | Web API |


The [`web.abort`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.abort.html) function allows you to stop a running simulation on the server and abort any associated data processing. Note that simply stopping the Python script or killing the kernel **won’t** stop the simulation in the cloud.

When you call `abort`, the server cancels the specified simulation and returns a `TaskInfo` object. This object contains details about the aborted simulation, including its status, size, and credit usage. The input parameter for [`web.abort`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.abort.html) is the **task_id**, not the [`Simulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html) object. This ID is returned by the [`web.upload`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.upload.html) method when a simulation is created.

## Example


```python
import tidy3d.web as web

# Abort the simulation
task_info = web.abort(task_id)

print("Simulation status:", task_info.status)
```


