# How do I create an adjoint parameterized level set optimization?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 22:43:05 | Inverse Design |


To create an adjoint parameterized level set-based optimization setup, you should use the design parameters as the control knots of a level set surface. Then, create a [CustomMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CustomMedium.html#tidy3d.CustomMedium) and set the permittivity values based on the zero level isocontour obtained from the level set surface. After that, include it in a [Structure](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Structure.html) object.

Once the simulation is defined, you can use the [web.run](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.run.html) method to send the simulation to our servers and process the data as usual.

 

Lastly, use <code>autograd.value_and_grad</code> to both compute the objective function and the gradient with respect to the design parameters. The objective function gradients can then feed a gradient-based optimization algorithm to drive the inverse design process. 

 

We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd10YBranchLevelSet/">tutorial</a> for an example on adjoint level set optimization.

 

 
