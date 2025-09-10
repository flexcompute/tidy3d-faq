# What is the formula for ContinuousWave?

| Date       | Category    |
|------------|-------------|
| 2025-09-05 17:29:25 | Sources |


The ContinuousWave sourcetime, if the DC component is zeroed out, has the following formula:
 
<center>
    $A(1+e^{-\frac{(t-t_o*t_w)}{t_w}})^{-1}e^{i\phi}e^{-i\omega_0 t}$
</center><br>
where $A$ is the amplitude, $t_o$ is the time offset, $t_w=\frac{1}{2\pi f_{width}}$ is the width of the pulse in seconds, $\phi$ is the phase shift, and $\omega_0=2\pi f_0$.
See the code [here](https://docs.flexcompute.com/projects/tidy3d/en/latest/_modules/tidy3d/components/source/time.html#ContinuousWave).