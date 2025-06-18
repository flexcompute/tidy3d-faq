---
_schema: default
title: How do I create an adjoint parameterized level set optimization?
date: 2023-12-21 22:43:05
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
To create an adjoint parameterized level set-based optimization setup, you should use the design parameters as the control knots of a level set surface. Then, create a [CustomMedium](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.CustomMedium.html#tidy3d.CustomMedium){: .color-primary-hover} and set the permittivity values based on the zero level isocontour obtained from the level set surface. After that, include it in a [Structure](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.Structure.html){: .color-primary-hover} object.

Once the simulation is defined, you can use the [web.run](https://docs.flexcompute.com/projects/tidy3d/en/v2.0.1/_autosummary/tidy3d.web.run.html){: .color-primary-hover} method to send the simulation to our servers and process the data as usual.

<div> </div>

<div>Lastly, use&nbsp;<code>Autograd.value_and_grad</code>&nbsp;to both compute the objective function and the gradient with respect to the design parameters. The objective function gradients can then feed a gradient-based optimization algorithm to drive the inverse design process.&nbsp;</div>

<div> </div>

<div>We highly recommend watching the <a href="https://www.flexcompute.com/tidy3d/learning-center/inverse-design/">Inverse Design</a> lectures if you are new to the adjoint method. You can also go through this <a href="https://www.flexcompute.com/tidy3d/examples/notebooks/Autograd10YBranchLevelSet/">tutorial</a> for an example on adjoint level set optimization.</div>

<div> </div>

<div> </div>
