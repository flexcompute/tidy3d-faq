---
title: Web.job?
date: 2025-09-16 13:50:36
enabled: true
category: "Web API"
---
[`web.Job`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.Job.html){: .color-primary-hover} is a lightweight container that represents a single simulation task on the Tidy3D cloud. It keeps track of the task ID, manages upload/start/monitor/download, and lets you save/load the job metadata without manually handling the original Simulation or task ID.

Use Job when working with one simulation and you want to track the task ID, conveniently manage simulations (upload/start/monitor/download), and have the ability to save/restore your job state cleanly across sessions.

Minimal Example

<div markdown class="code-snippet">
{% highlight python %}
from tidy3d.web.api.container import Job
from tidy3d import web

# Create a Job from an existing simulation
job = Job(simulation=simulation, task_name="my_task", folder_name="default")

# (Optional) Estimate cost before running
est = job.estimate_cost()
print(f"Estimated max cost (FC): {est:.2f}")

# Upload and start
job.upload()
job.start()
job.monitor()  # blocks until done

# Download and load results
sim_data = job.load(path="out/simulation.hdf5")

# Persist the job metadata for later reuse
job.to_file("data/job.json")

# Later (even in a new session), restore and load results:
job2 = Job.from_file("data/job.json")
sim_data2 = job2.load(path="data/simulation.hdf5")
{% endhighlight %}
{% include copy-button.html %}</div>

## Convenient methods

upload() – Upload the job (no run yet).

start() – Start running the job.

monitor() – Show progress until completion.

download(path) – Download results (.hdf5).

load(path) – Download and load as SimulationData.

estimate_cost(verbose=True) – Maximum FlexCredit estimate (assumes full run time).

real_cost(verbose=True) – Final billed cost.
