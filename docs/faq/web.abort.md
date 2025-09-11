# Web.abort?

| Date       | Category    |
|------------|-------------|
| 2025-09-11 18:22:50 | Web API |


The [`web.abort`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.abort.html) function allows you to stop a running task on the server and abort any associated data processing.

When you call `abort`, the server cancels the specified task and returns a `TaskInfo` object. This object contains details about the aborted task, including its status, size, and credit usage.

Note that the input parameter for [`web.abort`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.abort.html) is the **task_id**, not the [`Simulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html) object. This ID is returned by the [`web.upload`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.upload.html) method when a task is created.


## Example


```python
import tidy3d.web as web

# Abort the task
task_info = web.abort(task_id)

print("Task status:", task_info.status)
```


