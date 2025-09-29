# Web.run_async?

| Date       | Category    |
|------------|-------------|
| 2025-09-29 13:30:44 | Web API |


The [`web.run_async`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.web.run_async.html) function in Tidy3D allows you to submit and run multiple simulations in parallel on the server. It supports different simulation types (FDTD, Mode, HeatCharge, EME and RF) and automatically monitors, downloads, and loads the results into a [`web.BatchData`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.container.BatchData.html) object.



```python
batch_results = web.run_async(simulations=sims, verbose=verbose)
```



## For virtual GPU users

To run simulations in parallel, it is necessary to use your FlexCredit pool. To do this, set `pay_type = "FLEX_CREDITS"`:



```python
batch_results = web.run_async(simulations=sims, verbose=verbose,pay_type="FLEX_CREDITS")
```


