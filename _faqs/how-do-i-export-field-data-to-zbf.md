---
_schema: default
title: "How do I export field data to zbf?"
date: 2025-05-05 15:41:00
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
To export planar field monitor data to a Zemax beam file (.zbf), you can use&nbsp;`mon_data.to_zbf()`. For example:

<div><div markdown class="code-snippet">{% highlight python %}

# Run the simulation and get the data.
sim_data = tidy3d.web.run(simulation, task_name="task", path="data/data.hdf5", verbose=True)

# Save the data to a zbf file
ex, ey = sim_data['field_monitor'].to_zbf(
    fname='myzbf.zbf',
    background_refractive_index=1.0,
)

{% endhighlight %}

Detailed documentation can be found: &nbsp;[here](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.components.data.monitor_data.ElectromagneticFieldData.html#tidy3d.components.data.monitor_data.ElectromagneticFieldData.to_zbf)