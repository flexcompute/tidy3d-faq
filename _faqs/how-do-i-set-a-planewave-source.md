---
_schema: default
title: How do I set a PlaneWave source?
date: 2023-12-08 12:26:07
enable: true
category: Sources
_inputs:
  title:
    type: text
    label: QUESTION TITLE
  enable:
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
The&nbsp;[tidy3d.PlaneWave](https://docs.flexcompute.com/projects/tidy3d/en/latest/_autosummary/tidy3d.PlaneWave.html){: target="_blank" rel="noopener"}&nbsp;is a uniform current distribution on an infinite extent plane. The example below illustrates how to define a&nbsp;[tidy3d.PlaneWave](https://docs.flexcompute.com/projects/tidy3d/en/latest/_autosummary/tidy3d.PlaneWave.html){: target="_blank" rel="noopener"}&nbsp;within a simulation.

<div markdown class="code-snippet">{% highlight python %}

# Source bandwidth.
pulse = tidy3d.GaussianPulse(freq0=200e12, fwidth=20e12)

# Source definition
source = tidy3d.PlaneWave(
  center=(0, 0, 5),
  size=(tidy3d.inf, tidy3d.inf, 0),
  source_time=pulse,
  direction='-',
  pol_angle=np.pi/2,
  angle_theta=0,
  angle_phi=0,
  name="plane_wave",
)

{% endhighlight %}
{% include copy-button.html %}</div>

Use the `center`&nbsp;and `size` parameters to set the source position and dimension, then adjust the `source_time` dependence using [tidy3d.GaussianPulse](https://docs.flexcompute.com/projects/tidy3d/en/latest/_autosummary/tidy3d.GaussianPulse.html){: target="_blank" rel="noopener"}. The `direction` parameter specifies propagation in the positive or negative direction of the injection axis. You can change the light polarization using `pol_angle`, and&nbsp; adjust the propagation axis direction with `angle_theta`&nbsp;and&nbsp;`angle_phi`to control the polar and azimuth angles.

This [example](https://www.flexcompute.com/tidy3d/examples/notebooks/GratingEfficiency/) illustrates setting up a [tidy3d.PlaneWave](https://docs.flexcompute.com/projects/tidy3d/en/latest/_autosummary/tidy3d.PlaneWave.html){: target="_blank" rel="noopener"}&nbsp;source at normal and off-normal incidences.