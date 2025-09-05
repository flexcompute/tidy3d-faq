---
title: How Can I Save and Load a Fitted Medium?
date: 2025-09-05 17:21:49
enabled: true
category: "Mediums"
---
After fitting a medium, as described [here](https://docs.flexcompute.com/projects/tidy3d/en/stable/notebooks/Fitting.html){: .color-primary-hover}, it is possible to save the fitted medium as an hdf5 and save time when using it in another model. To save the file, just use the `.to_file` method:

<div markdown class="code-snippet">
{% highlight python %}
fitted_medium.to_file('medium_name.hdf5')
{% endhighlight %}
{% include copy-button.html %}</div>

Now, the saved medium can be loaded with the [PoleResidue](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.PoleResidue.html){: .color-primary-hover} `.from_file` method:

<div markdown class="code-snippet">
{% highlight python %}
loaded_medium = td.PoleResidue.from_file('medium_name.hdf5')
{% endhighlight %}
{% include copy-button.html %}</div>
