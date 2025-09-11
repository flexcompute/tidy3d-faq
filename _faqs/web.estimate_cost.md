---
title: Web.estimate_cost?
date: 2025-09-11 18:22:50
enabled: true
category: "Web API"
---
[`web.estimate_cost`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.estimate_cost.html){: .color-primary-hover} returns the **maximum** possible FlexCredit cost of running a simulation before it starts. This helps prevent accidentally launching overly expensive tasks.

The real cost after running the simulation can be checked with the [`web.real_cost`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.real_cost.html){: .color-primary-hover} method.

Note that the input parameter for `web.estimate_cost` and `web.real_cost` is the **task_id**, not the `Simulation` object. This ID is returned by the [`web.upload`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.upload.html){: .color-primary-hover} method when a task is created.

## Example
<div markdown class="code-snippet">
{% highlight python %}
from tidy3d import web

# Create a job and upload it
job = web.Job(simulation=sim, task_name="job_example", verbose=True)

# Estimate its maximum cost before running
estimated_cost = web.estimate_cost(job.task_id)
print(f"Estimated maximum cost: {estimated_cost:.3f} FlexCredits")
{% endhighlight %}
{% include copy-button.html %}</div>

A minimum simulation cost may apply, depending on task details.

The estimate is conservative: it assumes the simulation runs its full allocated time. For more information on the real cost and how to correctly estimate the simulation time, refer to [this](https://www.flexcompute.com/tidy3d/learning-center/tidy3d-gui/Lecture-8-Run-Time-and-Shutoff/){: .color-primary-hover} tutorial.

