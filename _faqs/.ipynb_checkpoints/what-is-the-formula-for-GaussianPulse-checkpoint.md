---
_schema: default
title: What is the formula for GaussianPulse?
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
The GaussianPulse sourcetime, if the DC component is zeroed out, has the following formula:
<div> </div>
<center>
    $(i+\frac{t}{t_w^2\omega_0})Ae^{i\phi}e^{-i\omega_0 t}e^{-\frac{(t - t_o*t_w)^2}{2t_w^2}}$
</center><br>
<div> </div>
<div>If the DC component is not zeroed out, the formula is</div><br>
<center>
    $iAe^{i\phi}e^{-i\omega_0 t}e^{-\frac{(t - t_o*t_w)^2}{2t_w^2}}$
</center><br>
<div>where $A$ is the amplitude, $t_o$ is the time offset, $t_w=\frac{1}{2\pi f_{width}}$ is the width of the pulse in seconds, $\phi$ is the phase shift, and $\omega_0=2\pi f_0$.</div>
<div>See the code [here](https://docs.flexcompute.com/projects/tidy3d/en/latest/_modules/tidy3d/components/source/time.html#GaussianPulse).</div>