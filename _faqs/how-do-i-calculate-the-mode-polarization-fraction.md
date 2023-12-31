---
_schema: default
title: How do I calculate the mode polarization fraction?
date: 2023-12-18 21:59:37
enable: true
category: Mode Solver
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
<div>You can follow the example below to obtain the mode polarization fraction of the optical modes calculated using the Tidy3D mode solver. We have considered a 500 x 220 nm silicon-on-insulator (SOI) waveguide operating at 1.55&nbsp;$\mu$m.</div>

<div> </div>

<div markdown class="code-snippet">{% highlight python %}
import numpy as np
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
  group_index_step=True,
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

print("TM polarization fraction:")
print(np.asarray(mode_data.pol_fraction['tm']).squeeze())

{% endhighlight %}
{% include copy-button.html %}</div>

<div><blockquote><p>The TE and TM polarization fractions are defined as the field intensity along the first or the second of the two tangential axes. More precisely, if&nbsp;<code>E1</code>&nbsp;and&nbsp;<code>E2</code>&nbsp;are the electric field components along the two tangential axes, the TE fraction is defined as&nbsp;<code>integrate(E1.abs**2) /&nbsp;integrate(E1.abs**2 +&nbsp;E2.abs**2)</code>, and the&nbsp;<code>TM</code>&nbsp;fraction is equal to one minus the TE fraction. The tangential axes are defined by popping the normal axis from the list of&nbsp;<code>x, y, z</code>, so e.g.&nbsp;<code>x</code>&nbsp;and&nbsp;<code>z</code>&nbsp;for propagation in the&nbsp;<code>y</code>&nbsp;direction.</p></blockquote><p>For more details on how to set up, run and visualize the solver results, please refer to this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/ModeSolver/">notebook</a>.</p></div>