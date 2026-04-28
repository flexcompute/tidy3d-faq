# Why Is My Tidy3d Notebook Storage Full If I Do Not See Large Files?

| Date       | Category    |
|------------|-------------|
| 2026-04-27 18:14:55 | About Tidy3D |


# Why is my Tidy3D notebook storage full if I do not see large files?

Your notebook storage may be full because hidden files or cache directories are using space. These files may not appear in the notebook file browser.



## How can I check what is using the space?

Run this command in the web notebook prompt:

find ~ -mindepth 1 -maxdepth 1 -exec du -sh {} + | sort -hr | head -n 10



```python
This shows the largest files and folders in your notebook environment, including hidden folders.
```



How can I clear the Tidy3D local cache?

Run this in a notebook cell:




```python
from tidy3d.web.cache import clear as clear_cache

clear_cache()
```



This clears the local Tidy3D cache, which is stored by default under:

`~/.cache/tidy3d/simulations`

This does not delete simulations from your cloud workspace.


Note: Notebook storage is separate from cloud workspace storage in [Folders](https://tidy3d.simulation.cloud/folders).
