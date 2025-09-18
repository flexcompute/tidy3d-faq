---
title: Web.get_tasks?
date: 2025-09-16 13:50:36
enabled: true
category: "Web API"
---
[`web.get_tasks`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.get_tasks.html){: .color-primary-hover} is a function in `tidy3d.web.api.webapi` that **retrieves metadata about past simulation tasks** from your account. It’s useful for reviewing recent runs, checking their IDs, and organizing workflows.

## What does it do?
- Returns a list of dictionaries with task metadata (e.g., ID, status, name).
- Lets you specify how many tasks to fetch and in what order.
- Can filter tasks by folder name.

## Example
<div markdown class="code-snippet">
{% highlight python %}
python
from tidy3d import web

# Get the 5 most recent tasks from the default folder
tasks = web.get_tasks(num_tasks=5, order="new", folder="default")

for t in tasks:
    print(f"Task {t['name']} (ID: {t['id']}) - Status: {t['status']}")
{% endhighlight %}
{% include copy-button.html %}</div>
