---
title: How Can I Continue a Adjoint Optmization?
date: 2025-06-19 14:55:02
enabled: true
category: "Inverse Design"
---
Using the `optax` library, it is possible to save and resume an adjoint optimization by recording the optimizer object state and the parameters from the last step. This allows you to either continue an ongoing optimization or extend a completed one with additional iterations.

The [Parameterized level set optimization of a y-branch](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd10YBranchLevelSet/){: .color-primary-hover} example illustrates this approach.
