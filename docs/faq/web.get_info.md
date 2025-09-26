# Web.get_info?

| Date       | Category    |
|------------|-------------|
| 2025-09-26 17:01:09 | Web API |


The [`web.get_info`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.get_info.html) function retrieves detailed information about a simulation. 

Given a *task_id* (returned when you upload a simulation), `get_info` returns a [`TaskInfo`](https://docs.flexcompute.com/projects/tidy3d/en/v2.5.1/_autosummary/tidy3d.web.core.task_info.TaskInfo.html) object. This object includes details such as whether the task is running or completed and how many FlexCredits were consumed. It’s useful for monitoring progress or checking costs after a run.

## Parameters
- **task_id** *(str)*: Unique identifier of the task on the server (returned by `web.upload`).
- **verbose** *(bool, default=True)*: If `True`, prints progress bars and status updates. If `False`, runs silently.

## Returns
- **TaskInfo**: An object containing status, size, and credit information for the task.

## Example


```python
from tidy3d import web

# Get task information
info = web.get_info(task_id)

print(info.status)   # e.g., "success"
print(info.realCost)  # e.g., 0.025
```


