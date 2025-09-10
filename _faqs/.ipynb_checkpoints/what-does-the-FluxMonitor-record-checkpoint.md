---
_schema: default
title: What does the FluxMonitor record?
date: 2025-09-08 17:29:25
enabled: true
category: Monitors
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
The FluxMonitor records field data tangential $E$ and $H$ fields colocated to the cell boundaries in the monitor's 2D plane grid. It then computes and integrates the Poynting vector, returning the real part of this integral as the flux.
<div> </div>
<center>
    Real$(\sum\limits_{\text{cells in monitor}}\frac{1}{2}(E_1\cdot H_2^*-E_2\cdot H_1^*)dA_{\text{cell}})$
</center><br>
where $dA$ is the area of each cell in the monitor, and the field components 1 and 2 are given depending on the monitor geometry: for $x$-normal monitors, 1 is $y$ and 2 is $z$; for $y$-normal monitors, 1 is $x$ and 2 is $z$; for $z$-normal monitors, 1 is $x$ and 2 is $y$. See the code [here](https://docs.flexcompute.com/projects/tidy3d/en/latest/_modules/tidy3d/components/data/monitor_data.html#ElectromagneticFieldData).