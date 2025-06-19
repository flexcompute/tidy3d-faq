# How many simulations are performed in adjoint calculations?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 21:14:12 | Inverse Design |


At least two simulations, the <code>forward</code> and the <code>adjoint</code> one, are performed when running inverse design optimizations using the <code>adjoint</code> plugin.

However, for **broadband** simulations, more than one <code>adjoint</code> simulation may be necessary depending on the type and number of monitors used.

- **Single-frequency differentiation**  
  If all monitors are set to differentiate at a single frequency, only **one adjoint simulation** is needed per forward simulation, regardless of how many monitors are present. This works because adjoint sources can be linearly combined.

- **Monitors with well-defined field profiles** (e.g., [ModeMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.ModeMonitor.html) or [DiffractionMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.DiffractionMonitor.html))  
  - **Single monitor**: One adjoint simulation per forward simulation is sufficient, even for broadband frequencies.  
  - **Multiple broadband monitors**: Multiple adjoint simulations may be needed. The plugin automatically selects the most efficient strategy:
    - Group single-frequency monitors into one adjoint simulation, or  
    - Run one adjoint simulation per monitor that includes all frequencies.

- **Monitors with arbitrary field profiles** (e.g., [FieldMonitor](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.FieldMonitor.html))  
  - These do not support broadband adjoint sources, so **one adjoint simulation is needed per frequency**.  
  - If multiple field monitors share the same frequency, they can be grouped into a single adjoint simulation.

Below is a summary of how the number of adjoint simulations depends on monitor type, frequency usage, and monitor count:

| Monitor Type           | Frequencies            | # of Monitors         | # of Adjoint Simulations                    |
||||---|
| Any                    | Single                 | Any                    | 1 per forward simulation                    |
| Mode / Diffraction     | Multiple               | 1                      | 1 per forward simulation                    |
| Mode / Diffraction     | Multiple               | >1                     | Depends (≤ #monitors or ≤ #frequencies)     |
| Field (arbitrary)      | Single                 | Any (same freq)        | 1                                           |
| Field (arbitrary)      | Multiple               | 1                      | = # of frequencies                          |
| Field (arbitrary)      | Multiple               | >1 (mixed freqs)       | = # of unique frequencies                   |

 

We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/">tutorial</a> for an introduction to the basic concepts related to automatic differentiation and adjoint optimization.

