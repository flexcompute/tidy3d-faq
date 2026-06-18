---
title: How Do I Save or Load a Tidy3d Parallel Job so I Can Work with It Later?
date: 2026-04-14 14:22:09
enabled: true
category: "Parameter Sweep"
---
# How do I save or load a multi-simulation task?

When using [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.run.html){: .color-primary-hover} on multiple simulations, a `batch.hdf5` file is automatically created at the path specified by the `path` argument of `web.run`. The default location is the current working directory.

You can load the object and data by calling the `web.Batch.from_file` and `load` methods:

<div markdown class="code-snippet">
{% highlight python %}
batch = web.Batch.from_file("path/batch.hdf5")
batch_data = batch.load()
{% endhighlight %}
{% include copy-button.html %}</div>

Note that after loading the data, the original data structure is not preserved, and the simulations are indexed by their API keys.
