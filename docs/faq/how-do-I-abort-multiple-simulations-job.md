# How Do I Abort Multiple Simulations Job?

| Date       | Category    |
|------------|-------------|
| 2026-04-10 16:29:38 | Parameter Sweep |


# How do I abort a job with multiple simulations?

When using [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.run.run.html) on multiple simulations, a `batch.hdf5` file is automatically created at the location specified by the `path` argument of `web.run`. The default location is the current working directory.

To abort the job, you can load the [`web.Batch`](https://docs.flexcompute.com/projects/tidy3d/en/v2.5.2/_autosummary/tidy3d.web.Batch.html) object and call the `delete` method:



```python
batch = web.Batch.from_file('path/batch.hdf5')
batch.delete()
```


