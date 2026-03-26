---
title: How to run a 2D simulation in Tidy3D?
date: 2023-12-03 21:00:22
enabled: true
category: "Simulations"
---
<div><div>To run 2D simulations in Tidy3D, set the simulation size in one dimension
to 0 (for example: <code>tidy3d.Simulation(size=[size_x, size_y, 0])</code>). Additionally, specify a <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Periodic.html">tidy3d.Periodic</a> boundary condition in that direction. 

Note that the structures should still be regular 3D structures.

For an example of running a 2D simulation in Tidy3D, see the <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/EffectiveIndexApproximation/">2D ring resonator notebook</a>.</div></div>
