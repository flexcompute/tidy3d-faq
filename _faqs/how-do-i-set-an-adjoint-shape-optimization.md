---
_schema: default
title: How do I set an adjoint shape optimization?
date: 2023-12-21 21:54:09
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
<div><p>To create an adjoint shape optimization setup, you need to provide <code>jax</code>-compatible geometries such as&nbsp;<a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.JaxBox.html">tidy3d.plugins.adjoint.JaxBox</a> or&nbsp;<a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.JaxPolySlab.html">tidy3d.plugins.adjoint.JaxPolySlab</a>&nbsp;when creating objects of type&nbsp;<a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.JaxStructure.html">tidy3d.plugins.adjoint.JaxStructure</a>. The structures should then be included in the&nbsp;<code>.input_structures</code>&nbsp;parameter of the&nbsp;<a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.JaxSimulation.html#tidy3d.plugins.adjoint.JaxSimulation">tidy3d.plugins.adjoint.JaxSimulation</a>&nbsp;object. In addition, you must specify an adjoint compatible monitor in&nbsp;<code>.output_monitors</code>, which defines the set of monitors and corresponding data that the objective function will depend on.</p>​​​​<span style="color: var(--color-carbon); font-family: var(--font-family); letter-spacing: 0.01rem;">Once the adjoint simulation is defined, you must use the&nbsp;</span><a target="_blank" rel="noopener" style="font-family: var(--font-family); letter-spacing: 0.01rem;" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.web.run.html">tidy3d.plugins.adjoint.web.run</a><span style="color: var(--color-carbon); font-family: var(--font-family); letter-spacing: 0.01rem;">&nbsp;method to send the simulation to our servers. After computing the forward and adjoint simulations, a&nbsp;</span><a target="_blank" rel="noopener" style="font-family: var(--font-family); letter-spacing: 0.01rem;" href="https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.plugins.adjoint.JaxSimulationData.html#tidy3d.plugins.adjoint.JaxSimulationData">tidy3d.plugins.adjoint.JaxSimulationData</a><span style="color: var(--color-carbon); font-family: var(--font-family); letter-spacing: 0.01rem;"> is returned, so you can compute the objective function value.&nbsp;</span></div>

<div> </div>

<div>Lastly, use&nbsp;<code>jax.value_and_grad</code>&nbsp;to both compute the objective function and the gradient with respect to the design parameters. The objective function gradients can then feed a gradient-based optimization algorithm to drive the inverse design process.&nbsp;</div>

<div> </div>

<div>We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/AdjointPlugin5BoundaryGradients/">tutorial</a> for an example on adjoint shape optimization.</div>

<div> </div>

<div> </div>