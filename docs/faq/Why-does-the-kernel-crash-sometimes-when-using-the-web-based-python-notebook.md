# Why does the kernel crash sometimes when using the web-based Python notebook?

| Date       | Category    |
|------------|-------------|
| 2023-10-24 18:09:43 | Simulation Troubleshoot |


The web-based Python notebook environment in `tidy3d.simulation.cloud` only has access to 4 GB of memory. When running a large simulation or complex optimizations, the memory needed to process the data could exceed the limit, causing the kernel to crash. In this case, we recommend installing `Tidy3D` on your local computer by following the installation [guide](https://docs.flexcompute.com/projects/tidy3d/en/latest/install.html) and [video](https://youtu.be/qQidx65Jmu0). It will then use your computer memory, which is typically larger than 4 GB.