---
title: Web.batch?
date: 2025-09-11 18:22:50
enabled: true
category: "Web API"
---
[`Batch`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.Batch.html){: .color-primary-hover} is a container for submitting, running, monitoring, and downloading **multiple simulations** on the Tidy3D cloud in one go. It’s similar to a [`web.Job`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.Job.html){: .color-primary-hover}, but for a whole set of tasks (FDTD, Heat/Charge, EME, Mode solver, etc.) that run in parallel.

## Estimating cost

It is possible to estimate the maximum cost of the whole batch with the `Batch.estimate_cost` method. For more information on simulation cost, check [this](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.6/faq/docs/faq/how-do-i-see-the-cost-of-my-simulation.html){: .color-primary-hover} article.

## Running a batch

The batch is run with the `Batch.run(path_dir="path_dir")` method, which saves a batch file that can be loaded later and returns a [BatchData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.BatchData.html){: .color-primary-hover} object.

## Loading a batch

A batch can be loaded using the `Batch.from_file` method. If the `Batch.run` method was previously used, the `Batch` object will contain information about all executed tasks, and the [BatchData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.BatchData.html){: .color-primary-hover} object can be returned with the `Batch.load` method. For more information, refer to [this](https://docs.flexcompute.com/projects/tidy3d/en/stable/faq/docs/faq/how-do-i-save-or-load-a-tidy3d-web-batch-so-i-can-work-with-it-later.html){: .color-primary-hover} article.

## When should I use it?

- Parameter sweeps, design-of-experiments, or any workflow with many related runs in parallel.

## Minimal example

<div markdown class="code-snippet">
{% highlight python %}
python
import tidy3d as td
from tidy3d.web.api.container import Batch

# 1) Build your simulations (FDTD shown as example)
sim_a = td.Simulation(...)  # define as usual
sim_b = td.Simulation(...)
sims = {"run_a": sim_a, "run_b": sim_b}

# 2) Create a Batch
batch = Batch(
    simulations=sims,
    folder_name="my_sweep",
)

# (Optional) Quick cost estimate (max, assuming full run_time)
est_fc = batch.estimate_cost(verbose=True)

# 3) Run (upload+start+monitor+download as needed)
data = batch.run(path_dir="results")

# 4) Iterate over results (lazy-loaded from disk, downloads on demand)
for name, sim_data in data.items():
    print(name, sim_data)
    # ... analyze sim_data ...

# 5) Access final billed cost later (after runs finish)
billed_fc = batch.real_cost(verbose=True)
print("Billed FlexCredits:", billed_fc)
{% endhighlight %}
{% include copy-button.html %}</div>
