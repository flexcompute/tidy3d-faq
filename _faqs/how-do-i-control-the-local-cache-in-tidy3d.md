---
title: How Do I Control the Local Cache in Tidy3d?
date: 2026-05-18 15:34:34
enabled: true
category: "Web API"
---
# How do I control the local cache in Tidy3D?

You can control the local cache in Tidy3D by setting `td.config.local_cache.enabled` to `True` or `False`.

<div markdown class="code-snippet">
{% highlight python %}
python
import tidy3d as td

td.config.local_cache.enabled = False  # Set to True to enable it again.
{% endhighlight %}
{% include copy-button.html %}</div>

Without saving, this change only applies to the current Python session. To keep the setting for future sessions, save the configuration:

<div markdown class="code-snippet">
{% highlight python %}
python
td.config.save()
{% endhighlight %}
{% include copy-button.html %}</div>

The local cache stores reusable simulation artifacts on your machine to avoid recomputing or re-downloading them when possible.