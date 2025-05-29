---
title: How can I simulate bent waveugides with EME?
date: 2025-05-27 18:52:21
enabled: true
category: "EME"
---
To simulate a **bent waveguide**, it is necessary to define the structure as **straight** in the geometry. The bend is then specified using the `bend_radius` parameter within the [`tidy3d.EMEModeSpec`](https://docs.flexcompute.com/projects/tidy3d/en/v2.7.3/api/_autosummary/tidy3d.EMEModeSpec.html){: target="_blank" rel="noopener"} object. In this setup, each EME cell represents a section with the given bend radius, allowing the solver to accurately account for curvature effects.

For a detailed example, refer to [this tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/EMEBends/){: target="_blank" rel="noopener"}.

