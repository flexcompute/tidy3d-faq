---
_schema: default
title: How do I calculate the power radiated by a PointDipole source?
date: 2023-12-08 11:40:56
enabled: true
category: Sources
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
The [tidy3d.PointDipole](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PointDipole.html) source placed in a lossless homogeneous material injects power close to the [analytically expected](https://docs.flexcompute.com/projects/tidy3d/en/latest/faq/docs/faq/How-are-results-normalized.html#source-power-normalization) result for an infinitesimal antenna with oscillating current. There can be a small difference from the analytical result due to the finite grid, which disappears in the limit of high resolution. To calculate the radiated power of a dipole in the presence of dispersive, lossy, or non-homogeneous materials, you can use a [tidy3d.FluxMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FluxMonitor.html) box. Refer to this [notebook](https://www.flexcompute.com/tidy3d/examples/notebooks/BullseyeCavityPSO/) for an example.