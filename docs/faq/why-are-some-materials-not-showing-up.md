# Why are some materials not showing up?

| Date       | Category    |
|------------|-------------|
| 2025-07-17 13:05:34 | Simulation Troubleshoot |


Tidy3D resolves material overlap by their priority - see [here](https://docs.flexcompute.com/projects/tidy3d/en/latest/faq/docs/faq/when-two-structures-overlap-what-is-the-priority-determined.html) for details.

If the priority matches what is needed and the material overlap still does not appear, be sure to check symmetry settings, as the specified symmetry must match the structure symmetry of the simulation.
