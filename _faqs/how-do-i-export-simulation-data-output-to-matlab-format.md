---
_schema: default
title: "How do I export Simulation data output to MATLAB format?"
date: 2025-02-05 13:47:06
enabled: true
category: Data Visualization and Postprocessing
_inputs:
  title:
    type: text
    label: QUESTION TITLE
  enabled:
    type: switch
    hidden: true
  date:
    type: datetime
    label: DATE
    instance_value: NOW
  category:
    type: select
    options:
      values: data.faq_categories
      value_key: key
      preview:
        text:
          - key: category_name
---
You can use the&nbsp;[SimulationData.to_mat_file]( https://docs.flexcompute.com/projects/tidy3d/en/stable/api/_autosummary/tidy3d.components.data.sim_data.SimulationData.html#tidy3d.components.data.sim_data.SimulationData.to_mat_file){: target="_blank" rel="noopener"}&nbsp;function to export simulation data in MATLAB format. For example:

<div><div markdown class="code-snippet">{% highlight python %}

# Run the simulation and get the data.
sim_data = tidy3d.web.run(simulation, task_name="task", path="data/data.hdf5", verbose=True)

# Export to MATLAB format.
sim_data.to_mat_file('/path/to/file/data.mat') 

{% endhighlight %}
{% include copy-button.html %}</div><p>You can find detailed information about simulation data visualization and postprocessing in this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/VizData/">tutorial</a>.</p></div>
