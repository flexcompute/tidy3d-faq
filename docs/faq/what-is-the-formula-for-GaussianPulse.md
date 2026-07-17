# What is the formula for GaussianPulse?

| Date       | Category    | Version |
|------------|-------------|---------|
| 2026-07-16 09:00:00 | Sources | 2.10 |


The [GaussianPulse](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.GaussianPulse.html) source time, if the DC component is zeroed out (`remove_dc_component=True`, the default), has the following formula (valid for Tidy3D 2.10 and later):

$$\frac{i\omega_0+\frac{t_s}{t_w^2}}{2\pi f_{peak}}Ae^{i\phi}e^{-i\omega_0 t}e^{-\frac{t_s^2}{2t_w^2}}$$

where $t_s = t - t_o t_w$ is the shifted time and the normalization frequency $f_{peak}$ is the frequency at which the pulse spectrum reaches its peak amplitude,

$$f_{peak}=\frac{f_0+\sqrt{f_0^2+4f_{width}^2}}{2}$$

If the DC component is not zeroed out, the formula is

$$iAe^{i\phi}e^{-i\omega_0 t}e^{-\frac{t_s^2}{2t_w^2}}$$

where $A$ is the amplitude, $t_o$ is the time offset, $t_w=\frac{1}{2\pi f_{width}}$ is the width of the pulse in seconds, $\phi$ is the phase shift, and $\omega_0=2\pi f_0$.

See the code [here](https://docs.flexcompute.com/projects/tidy3d/en/latest/_modules/tidy3d/components/source/time.html#GaussianPulse).
