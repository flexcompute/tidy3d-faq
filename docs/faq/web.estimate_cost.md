# Web.estimate_cost?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 13:50:36 | Web API |


[`web.estimate_cost`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.estimate_cost.html) returns the **maximum** possible FlexCredit cost of running a simulation before it starts. This helps prevent accidentally launching overly expensive simulations.

The real cost after running the simulation can be checked with the [`web.real_cost`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.real_cost.html) method.

Note that the input parameter for `web.estimate_cost` and `web.real_cost` is the **task_id**, not the `Simulation` object. This ID is returned by the [`web.upload`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.upload.html) method when a simulation is created.

## Example


```python
from tidy3d import web

# Create a job and upload it
job = web.Job(simulation=sim, task_name="job_example", verbose=True)

# Estimate its maximum cost before running
estimated_cost = web.estimate_cost(job.task_id)
print(f"Estimated maximum cost: {estimated_cost:.3f} FlexCredits")
```



A minimum simulation cost may apply, depending on simulation details.

The estimate is conservative: it assumes the simulation runs its full allocated time. For more information on the real cost and how to correctly estimate the simulation time, refer to [this](https://www.flexcompute.com/tidy3d/learning-center/tidy3d-gui/Lecture-8-Run-Time-and-Shutoff/) tutorial.

