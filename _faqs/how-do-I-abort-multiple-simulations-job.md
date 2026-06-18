---
title: How Do I Abort Multiple Simulations Job?
date: 2026-04-14 14:22:09
enabled: true
category: "Parameter Sweep"
---
# How do I abort a job with multiple simulations?

When using [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.run.html){: .color-primary-hover} on multiple simulations, a `batch.hdf5` file is automatically created at the location specified by the `path` argument of `web.run`. The default location is the current working directory.

To abort the job, you can load the [`web.Batch`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.Batch.html){: .color-primary-hover} object and call the `delete` method:

<div markdown class="code-snippet">
{% highlight python %}
batch = web.Batch.from_file('path/batch.hdf5')
batch.delete()
{% endhighlight %}
{% include copy-button.html %}</div>
