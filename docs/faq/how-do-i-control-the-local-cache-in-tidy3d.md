# How Do I Control the Local Cache in Tidy3d?

| Date       | Category    |
|------------|-------------|
| 2026-05-18 15:34:34 | Web API |


# How do I control the local cache in Tidy3D?

You can control the local cache in Tidy3D by setting `td.config.local_cache.enabled` to `True` or `False`.



```python
python
import tidy3d as td

td.config.local_cache.enabled = False  # Set to True to enable it again.
```



Without saving, this change only applies to the current Python session. To keep the setting for future sessions, save the configuration:



```python
python
td.config.save()
```



The local cache stores reusable simulation artifacts on your machine to avoid recomputing or re-downloading them when possible.