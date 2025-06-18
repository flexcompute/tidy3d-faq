---
_schema: default
title: How do I set an inverse design problem?
date: 2023-12-21 19:01:14
enabled: true
category: Inverse Design
_inputs:
  title:
    type: text
    label: QUESTION TITLE
  enabled:
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
With Tidy3D's integration with `Autograd`, setting up an inverse design workflow is straightforward.

All you need to do is define a function to create the [`Simulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html){: .color-primary-hover} object as a function of the optimization parameters, run the simulation, post-process the data, and return the cost function. Once this function is defined, you can call `Autograd.value_and_grad` to run the simulation and obtain the gradients.

### General Workflow

1. **Create a `make_sim` function**  
   This function takes in the optimization parameters and returns a [`Simulation`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Simulation.html){: .color-primary-hover} object.

2. **Define a post-processing function**  
   This function calculates the objective (cost) function from the resulting [`SimulationData`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.components.data.sim_data.SimulationData.html){: .color-primary-hover} object.

3. **Wrap it all in a single function**  
   This wrapper receives the optimization parameters, creates and runs the simulation, applies the post-processing, and returns the objective function.

4. **Use `Autograd.value_and_grad`**  
   Input the wrapper function into `Autograd.value_and_grad` to obtain both the cost function value and its derivatives. These gradients can then be used in a gradient-based optimization algorithm to guide the inverse design process.

We highly recommend watching the [Inverse Design lectures](https://www.flexcompute.com/tidy3d/learning-center/inverse-design/){: .color-primary-hover} if you're new to the adjoint method. You can also explore this [tutorial](https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd1Intro/){: .color-primary-hover} for an introduction to automatic differentiation and adjoint optimization.
