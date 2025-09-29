# Web.delete_old?

| Date       | Category    |
|------------|-------------|
| 2025-09-29 11:29:13 | Web API |


The [`web.delete_old`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.delete_old.html) function is used to automatically clean up older simulation tasks stored on the server. It helps manage storage by removing tasks that are no longer needed after a certain number of days.

## What does it do?
Given a time threshold in days, the function deletes all tasks older than that age in a specified folder. This makes it easy to clear out outdated simulations without manually deleting them one by one.
Be aware that deleted tasks *can't be recovered*.

- **int**: The total number of tasks deleted.

## Example



```python
from tidy3d import web

# Delete all tasks older than 60 days in the default folder
num_deleted = web.delete_old(days_old=60)

print(f"Deleted {num_deleted} old tasks.")
```



## Parameters
- **days_old** *(int, default=100)*: Minimum number of days since task creation. Tasks older than this will be deleted.
- **folder** *(str, default="default")*: Folder where the deletion will occur. Only one folder can be specified at a time.
