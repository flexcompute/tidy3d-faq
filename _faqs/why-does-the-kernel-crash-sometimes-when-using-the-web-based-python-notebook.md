---
title: Why does the kernel crash sometimes when using the web-based Python notebook?
date: 2023-10-24 18:09:43
enabled: true
category: 'Simulation Troubleshoot'
---
The web-based Python notebook environment in `tidy3d.simulation.cloud` only has access to 8 GB of memory. When running a large simulation or complex optimizations, the memory needed to process the data could exceed the limit, causing the kernel to crash. In this case, we recommend installing `Tidy3D` on your local computer by following the installation [guide](https://docs.flexcompute.com/projects/tidy3d/en/latest/install.html) and [video](https://youtu.be/qQidx65Jmu0). It will then use your computer memory, which is typically larger than 8 GB.

If symmetries are not used in the simulation, memory usage can be reduced by calling `data = sim_data.monitor_data['monitor_name']` instead of `data = sim_data['monitor_name']`. The latter creates a copy of the monitor data and expands it to include the symmetric parts, if applicable.

However, if symmetries are used in the simulation, `data = sim_data.monitor_data['monitor_name']` will return data only for the simulated portion of the volume, and not the symmetric extensions. For example, if symmetry is applied in the x-plane, only half of the data will be returned.

Note that many analyses can still be performed with this partial data. For instance, the mode volume can be computed using the non-expanded monitor and then multiplied by the appropriate factor (`2`, `4`, or `8` for `1`, `2`, or `3` symmetry planes, respectively).

