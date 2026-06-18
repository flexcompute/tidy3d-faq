---
title: How to Iterate Through Results From Multiple Simulations Without Loading All of the Data Into Memory?
date: 2026-04-14 14:22:09
enabled: true
category: "Parameter Sweep"
---
# How to iterate through results from a multi-simulation `web.run` workflow?

When using [`web.run`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.run.html){: .color-primary-hover} on multiple simulations, the returned object preserves the **same input structure**. This works for dictionaries, lists, tuples, and nested combinations of them.

For example, when `web.run` is called on a dictionary of simulations, the returned object can be iterated over by task name:

<div markdown class="code-snippet">
{% highlight python %}
from tidy3d import web

sims = {
    "sim_1": sim_1,
    "sim_2": sim_2,
    "sim_3": sim_3,
}

results = web.run(sims, verbose=True)

for task_name, sim_data in results.items():
    print(task_name)
    print(sim_data)
{% endhighlight %}
{% include copy-button.html %}</div>

This gives access to each [SimulationData](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.SimulationData.html){: .color-primary-hover} object for postprocessing.

`web.run` also supports other input structures. For example, if the input is a list of simulations, the output is a list of results in the same order. If the input is a nested combination, such as a list of dictionaries or a nested list, the output keeps that same structure, making it straightforward to iterate through each group in a way that matches the original parameter scan.

You can find more examples on [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/ParameterScanWebRun){: .color-primary-hover}.
