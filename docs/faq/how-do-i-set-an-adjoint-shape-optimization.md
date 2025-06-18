# How do I set an adjoint shape optimization?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 21:54:09 | Inverse Design |


To create an adjoint shape optimization setup, you can use parametric structures such as [`Box`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Box.html) or [`PolySlab`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PolySlab.html) that are defined as functions of the optimization parameters.

Additionally, it is possible to apply operations such as rotation, translation, and boolean operations to further manipulate the geometry.

 

Lastly, use <code>Autograd.value_and_grad</code> to compute both the objective function and the gradient with respect to the design parameters. The objective function gradients can then feed a gradient-based optimization algorithm to drive the inverse design process.

 

We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd5BoundaryGradients/">tutorial</a> for an example of adjoint shape optimization.

 

 
