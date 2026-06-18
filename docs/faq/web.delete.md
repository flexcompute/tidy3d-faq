# Web.delete?

| Date       | Category    |
|------------|-------------|
| 2025-09-29 13:30:44 | Web API |


The [`web.delete`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.delete.html) function in Tidy3D is used to remove simulation stored on the server. This is useful for managing storage and ensuring that old or unnecessary tasks don’t take up space.

## What does it do?
Given a *task_id*, the function deletes the corresponding simulation. You can choose to delete only the specific version of the task or all versions within the same task group.

## Example


```python
from tidy3d import web

# Delete only this version
web.delete(task_id)

# Delete all versions of the task group
web.delete(task_id, versions=True)
```



## Parameters
- **task_id** *(str)*: Unique identifier of the task on the server (returned by `web.upload`).
- **versions** *(bool, default=False)*:  
  - `False`: Deletes only the task version associated with the given *task_id*.  
  - `True`: Deletes all versions of the task in the task group.

## Returns
- **TaskInfo**: An object containing information about the task status, size, and credit usage.
