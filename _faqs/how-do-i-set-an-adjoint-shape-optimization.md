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
To create an adjoint shape optimization setup, you can use parametric structures such as [`Box`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Box.html){: .color-primary-hover} or [`PolySlab`](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PolySlab.html){: .color-primary-hover} that are defined as functions of the optimization parameters.

Additionally, it is possible to apply operations such as rotation, translation, and boolean operations to further manipulate the geometry.

<div> </div>

<div>Lastly, use <code>Autograd.value_and_grad</code> to compute both the objective function and the gradient with respect to the design parameters. The objective function gradients can then feed a gradient-based optimization algorithm to drive the inverse design process.</div>

<div> </div>

<div>We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd5BoundaryGradients/">tutorial</a> for an example of adjoint shape optimization.</div>

<div> </div>

<div> </div>
