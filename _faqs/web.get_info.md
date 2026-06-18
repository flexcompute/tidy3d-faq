---
title: Web.get_info?
date: 2025-09-29 13:30:44
enabled: true
category: "Web API"
---
The [`web.get_info`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.get_info.html){: .color-primary-hover} function retrieves detailed information about a simulation.

Given a *task_id* (returned when you upload a simulation), `get_info` returns a [`TaskInfo`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.core.task_info.TaskInfo.html){: .color-primary-hover} object. This object includes details such as whether the task is running or completed and how many FlexCredits were consumed. It’s useful for monitoring progress or checking costs after a run.

## Parameters
- **task_id** *(str)*: Unique identifier of the task on the server (returned by `web.upload`).
- **verbose** *(bool, default=True)*: If `True`, prints progress bars and status updates. If `False`, runs silently.

## Returns
- **TaskInfo**: An object containing status, size, and credit information for the task.

## Example
<div markdown class="code-snippet">
{% highlight python %}
from tidy3d import web

# Get task information
info = web.get_info(task_id)

print(info.status)   # e.g., "success"
print(info.realCost)  # e.g., 0.025
{% endhighlight %}
{% include copy-button.html %}</div>
