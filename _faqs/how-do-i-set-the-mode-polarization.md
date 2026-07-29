---
title: How Do I Set the Mode Polarization?
date: 2026-04-28 18:51:48
enabled: true
category: "Mode Solver"
---
After running the Tidy3D <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolver.html#tidy3d.plugins.mode.ModeSolver">mode solver</a>, the results are returned within a <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.mode.ModeSolverData.html#tidy3d.plugins.mode.ModeSolverData">ModeSolverData</a> object. The solver computes the <code>num_modes</code> modes closest to the given <code>target_neff</code>. By default, modes are sorted by decreasing effective index.

To prioritize modes with a desired polarization, use <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/mode/_autosummary/tidy3d.ModeSortSpec.html#tidy3d.ModeSortSpec"><code>tidy3d.ModeSortSpec</code></a> through <code>ModeSpec.sort_spec</code>. For example, to return TE-like modes first, set <code>filter_key="TE_fraction"</code>, <code>filter_reference=0.5</code>. Modes with TE fraction greater than or equal to 0.5 are placed first, followed by the remaining modes. Within each group, modes use the default ordering by decreasing effective index.

The example below shows how to set the mode solver to return the TE modes first in the mode list.

<div markdown class="code-snippet">
{% highlight python %}
import numpy as np
import tidy3d
from tidy3d.plugins.mode import ModeSolver
from tidy3d.plugins.mode.web import run as run_mode_solver

# Define the waveguide.
waveguide = tidy3d.Structure(
    geometry=tidy3d.Box(size=(tidy3d.inf, 0.5, 0.22)),
    medium=tidy3d.Medium(permittivity=3.47**2),
)

# Build a simulation object including the waveguide.
sim = tidy3d.Simulation(
    size=(10, 2.5, 1.5),
    grid_spec=tidy3d.GridSpec.auto(min_steps_per_wvl=20, wavelength=1.55),
    structures=[waveguide],
    run_time=1e-12,
    boundary_spec=tidy3d.BoundarySpec.all_sides(boundary=tidy3d.PML()),
)

# Plane where we want to solve the modes.
plane = tidy3d.Box(center=(0, 0, 0), size=(0, 2.5, 1.5))

# Mode specification.
mode_spec = tidy3d.ModeSpec(
    num_modes=4,
    target_neff=3.47,
    sort_spec=tidy3d.ModeSortSpec(
        filter_key="TE_fraction",
        filter_reference=0.5,
    ),
)

# Build the mode solver.
freq0 = tidy3d.C_0 / 1.55
mode_solver = ModeSolver(
    simulation=sim,
    plane=plane,
    mode_spec=mode_spec,
    freqs=[freq0],
)

# Run the server-side mode solver.
mode_data = run_mode_solver(mode_solver)

# Get the mode polarization fraction.
print("TE polarization fraction:")
print(np.asarray(mode_data.pol_fraction['te']).squeeze())
{% endhighlight %}
{% include copy-button.html %}</div>
