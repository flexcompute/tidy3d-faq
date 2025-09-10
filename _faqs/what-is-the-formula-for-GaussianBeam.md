---
_schema: default
title: What is the formula for GaussianBeam?
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
The GaussianBeam source has the following scalar field amplitude, in cylindrical coordinates:
<div> </div>
<center>
    $u(r,z)=\frac{w_0}{w(z)}e^{-\frac{r^2}{w(z)^2}}e^{i(zk_0 + \frac{r^2k_0}{2R(z)} - \psi_g)}$
</center><br>
where:
<ul>
    <li>$z$ is the propagation direction</li>
    <li>$k_0=\frac{2\pi nf}{c}$ are the wavenumbers of the frequencies $f$ where the beam is sampled</li>
    <li>$w_0$ is the beam waist</li>
    <li>$w(z)=w_0\sqrt{1 + \frac{(z + z_0)^2}{z_r}}$, where $z_0$ is the waist distance and $z_r=\frac{1}{2}w_0^2k_0$ is the Rayleigh range</li>
    <li>$R(z)=z(1 + (\frac{z_r}{z})^2)$ is the radius of curvature of the wavefront at $z$</li>
    <li>$\psi_g=\arctan(\frac{z+z_0}{z_r})-\arctan(\frac{z_0}{z_r})$ is the Gouy phase</li>
</ul>

<div>See the code [here](https://docs.flexcompute.com/projects/tidy3d/en/latest/_modules/tidy3d/components/beam.html#GaussianBeamProfile).</div>