# How do I set an adjoint topology optimization?

| Date       | Category    |
|------------|-------------|
| 2023-12-21 22:12:45 | Inverse Design |


To create an adjoint topology (or density-based) optimization setup, you can control the permittivity values of a [CustomMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CustomMedium.html) based on the optimization design parameters. 

Once the simulation is defined, you can use the [web.run](https://docs.flexcompute.com/projects/tidy3d/en/v2.0.1/_autosummary/tidy3d.web.run.html) method to send the simulation to our servers and process the data as usual.


 

Lastly, use <code>autograd.value_and_grad</code> to both compute the objective function and the gradient with respect to the design parameters. The objective function gradients can then feed a gradient-based optimization algorithm to drive the inverse design process. 

 

We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd6GratingCoupler/">tutorial</a> for an example on adjoint topology optimization.

 

 
