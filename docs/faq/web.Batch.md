# Web.batch?

| Date       | Category    |
|------------|-------------|
| 2025-09-16 13:50:36 | Web API |


[`Batch`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.Batch.html) is a container for submitting, running, monitoring, and downloading **multiple simulations** on the Tidy3D cloud in one go. It’s similar to a [`web.Job`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.Job.html), but for a whole set of simulations (FDTD, Heat/Charge, EME, Mode solver, etc.) that run in parallel.

## Estimating cost

It is possible to estimate the maximum cost of the whole batch with the `Batch.estimate_cost` method. For more information on simulation cost, check [this](https://docs.flexcompute.com/projects/tidy3d/en/latest/faq/docs/faq/how-do-i-see-the-cost-of-my-simulation.html) article.

## Running a batch

The batch is run with the `Batch.run(path_dir="path_dir")` method, which saves a batch file that can be loaded later and returns a [BatchData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.BatchData.html) object.

## Loading a batch

A batch can be loaded using the `Batch.from_file` method. If the `Batch.run` method was previously used, the `Batch` object will contain information about all executed tasks, and the [BatchData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.BatchData.html) object can be returned with the `Batch.load` method. For more information, refer to [this](https://docs.flexcompute.com/projects/tidy3d/en/stable/faq/docs/faq/how-do-i-save-or-load-a-tidy3d-web-batch-so-i-can-work-with-it-later.html) article.

## When should I use it?

- Parameter sweeps, design-of-experiments, or any workflow with many related runs in parallel.

## Minimal example



```python
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
```


