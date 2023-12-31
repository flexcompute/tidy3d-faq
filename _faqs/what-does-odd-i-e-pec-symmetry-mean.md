---
_schema: default
title: What does “odd, i.e. ‘PEC’ symmetry” mean?
date: 2023-12-15 16:25:04
enable: true
category: Symmetry
_inputs:
  title:
    type: text
    label: QUESTION TITLE
  enable:
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
PEC symmetry (odd) corresponds to zero normal electric field and zero tangential magnetic field at the symmetry plane.

![](/uploads/pec-1.png){: width="223" height="485"}