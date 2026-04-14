# How Do I Run a Parameter Sweep?

| Date       | Category    |
|------------|-------------|
| 2026-04-14 14:22:09 | Parameter Sweep |


# How do I run a parameter sweep?

[`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.run.run.html) is the unified interface for running simulations on the Tidy3D cloud.

For parameter sweeps and multi-simulation workflows, `web.run` accepts not only a single simulation, but also dictionaries, lists, tuples, and nested combinations of these.

As shown in [ParameterScanWebRun.ipynb](https://www.flexcompute.com/tidy3d/examples/notebooks/ParameterScanWebRun), using a dictionary is convenient because each dictionary key is preserved as the task name in the returned results mapping.

## When should I use it?

- Parameter sweeps
- Design of experiments workflows
- Any scripted workflow involving many related simulations

## Running many simulations

Create a dictionary of simulations and pass it directly to `web.run`:



```python
import tidy3d as td
from tidy3d import web

sims = {
    "run_a": sim_a,
    "run_b": sim_b,
}

results = web.run(sims, path = 'sweep')
```



Here, web.run handles submission, monitoring, and loading of all simulations in one call.

## Accessing results

The returned object can be indexed by task name or iterated over:



```python
sim_data_a = results["run_a"]

for task_name, sim_data in results.items():
    print(task_name, sim_data)
```



This makes web.run a natural choice for parameter sweeps where task naming is derived from parameter values.

### Related note

Older workflows may use tidy3d.web.Batch for multi-simulation execution. web.run provides a simpler unified interface for the workflow shown in [ParameterScanWebRun.ipynb](https://www.flexcompute.com/tidy3d/examples/notebooks/ParameterScan).
