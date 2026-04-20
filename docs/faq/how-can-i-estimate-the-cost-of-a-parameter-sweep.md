# How Can I Estimate the Cost of a Parameter Sweep?

| Date       | Category    |
|------------|-------------|
| 2026-04-14 14:22:09 | Parameter Sweep |


# How can I estimate the cost of a parameter sweep?

When running multiple simulations, you can estimate the total cost before submission using `web.Batch(...).estimate_cost()`.

If your simulations are stored in nested structures (lists, tuples, dictionaries), first flatten them into a dictionary.

## Example



```python
from tidy3d import web

def flatten_sims(sims, flat=None, prefix=\"sim\"):
    if flat is None:
        flat = {}

    if isinstance(sims, dict):
        for v in sims.values():
            flatten_sims(v, flat, prefix)
    elif isinstance(sims, (list, tuple)):
        for v in sims:
            flatten_sims(v, flat, prefix)
    else:
        flat[f\"{prefix}_{len(flat)}\"] = sims

    return flat

flat_sims = flatten_sims(sims)

cost = web.Batch(simulations=flat_sims).estimate_cost()
print(cost)
```



This works for any combination of nested dictionaries, lists, or tuples.
