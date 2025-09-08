---
_schema: default
title: What is the formula for PlaneWave?
date: 2025-09-05 17:29:25
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
The PlaneWave source has the following scalar field amplitude:
<div> </div>
<center>
    $u(z)=e^{ik_z z}$
</center><br>
where $z$ is the propagation direction and $k_0=\frac{2\pi nf}{c}$ are the wavenumbers of the frequencies $f$ where the beam is sampled. If the source is specified as a fixed angle source, $k_0$ is multiplied by $\cos\theta$.

<div>See the code [here](/https://docs.flexcompute.com/projects/tidy3d/en/latest/_modules/tidy3d/components/beam.html#PlaneWaveBeamProfile).</div>