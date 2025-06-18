# How is the adjoint simulation billed?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 21:19:39 | Inverse Design |


Both the `forward` and the `adjoint` simulations are billed when running inverse design optimizations using the `autograd` plugin. That represents a significant reduction in computational cost, as the adjoint method allows one to calculate the gradient of an objective function with respect to thousands of design parameters using only two simulations in the simplest case.

The number of adjoint simulations — and thus the billing — depends on the monitor type, the number of monitors, and the number of frequencies involved:

- **Single-frequency differentiation**:  
  If all monitors are configured to differentiate at a single frequency, only one adjoint simulation is needed per forward simulation, regardless of how many monitors are present. This is possible because the adjoint sources can be combined via linear superposition.

- **Monitors with well-defined field profiles** (e.g., `mode` or `directivity` calculations):  
  - If differentiating with respect to a single monitor, only one adjoint simulation is needed per forward simulation — even for broadband frequencies.  
  - If multiple broadband monitors are used, multiple adjoint simulations may be required. The adjoint plugin automatically chooses the most efficient strategy:
    - Group monitors with a single frequency into one adjoint simulation (single-frequency case), or  
    - Run one simulation per monitor including all frequencies (broadband case).

- **Monitors with arbitrary field profiles** (e.g., `field` monitors):  
  - These do not support broadband adjoint sources, so one adjoint simulation is required per frequency.  
  - Multiple field monitors with the same frequency can still be grouped into a single adjoint simulation.

Each adjoint simulation typically costs approximately the same as the corresponding forward simulation. The total cost is therefore proportional to the number of adjoint simulations required.

Below is a table summarizing how the number of adjoint simulations depends on the type of monitor, the number of frequencies, and the number of monitors used in the optimization:

| Monitor Type            | Frequencies           | # of Monitors       | # of Adjoint Simulations                    |
|-|||
| Any                     | Single                | Any                  | 1 per forward simulation                    |
| Mode / Directivity      | Multiple              | 1                    | 1 per forward simulation                    |
| Mode / Directivity      | Multiple              | >1                   | Depends (≤ #monitors or ≤ #frequencies)     |
| Field (arbitrary)       | Single                | Any (same freq)      | 1                                           |
| Field (arbitrary)       | Multiple              | 1                    | = # of frequencies                          |
| Field (arbitrary)       | Multiple              | >1 (mixed freqs)     | = # of unique frequencies                   |

We highly recommend watching the [Inverse Design](https://www.flexcompute.com/tidy3d/learning-center/inverse-design/) lectures if you are new to the adjoint method. You can also go through this [tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/) for an introduction to the basic concepts related to automatic differentiation and adjoint optimization.
