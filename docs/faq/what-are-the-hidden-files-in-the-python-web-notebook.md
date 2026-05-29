# What are the Hidden Files in the Python Web Notebook?

| Date       | Category    |
|------------|-------------|
| 2026-05-28 16:41:10 | About Tidy3D |


# What Are the Hidden Files in the Python Web Notebook?

When you open the storage popover in the Tidy3D Python Web Notebook, you'll see your usage broken into:

- **Notebook Total Usage** — everything in your notebook environment.
- **Simulation Files** — your notebook, scripts, and other simulation files such as `.hdf5` / `.json` files you've saved from [web.run()](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.run.html) and similar calls, visible in the file browser.
- **Hidden Files** — everything else in your home directory that doesn't show up in the file browser by default.
- **Notebook Storage Limit** — your account's storage quota for this notebook environment (separate from your cloud workspace).

This FAQ explains what those hidden files are, how to see them, and how to free space when they grow large.



## What are hidden files?

Hidden files and folders are entries whose name starts with a dot (`.cache`, `.jupyter`, `.local`, `.ipynb_checkpoints`, `.git`, `.config`, …). The notebook file browser hides them by default to keep the view focused on your work.

They are created automatically by the notebook and by Tidy3D itself, and typically include:

- `.cache/tidy3d/` — the local Tidy3D simulation cache. Stores results of [web.run()](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.run.html) so re-running the same simulation doesn't re-download or re-execute it. This is usually the largest contributor.
- `.ipynb_checkpoints/` — JupyterLab auto-save snapshots of your notebooks.
- `.jupyter/`, `.local/`, `.config/` — JupyterLab and Python package settings.
- `.git/` — if a folder is a git repository, this stores its history.

These files are normal — they're not leftover junk and you don't need to manage them day-to-day. But they do count toward your **Notebook Storage Limit**, which is why they appear in the storage popover.



## How do I show or hide them?

In the notebook menu bar:

**View → Show Hidden Files**

Toggling it on shows all dotfiles and dotfolders in the file browser; toggling it off restores the default clean view. The setting is per-session.



## How do I see what's actually using my space?

Open a terminal in the notebook (**File → New → Terminal**) and run:



```python
bash
find ~ -mindepth 1 -maxdepth 1 -exec du -sh {} + | sort -hr | head -n 10
```



This lists the ten largest items in your home directory, including hidden folders, so you can see which one is responsible for the usage.

See: [Why is my Tidy3D notebook storage full if I do not see large files?](https://docs.flexcompute.com/projects/tidy3d/en/latest/faq/docs/faq/why-is-my-tidy3d-notebook-storage-full-if-i-do-not-see-large-files.html)



## How do I clear the Tidy3D local cache?

If `.cache/tidy3d/` is large and you don't need its contents, clear it from a notebook cell:



```python
python
from tidy3d.web.cache import clear as clear_cache

clear_cache()
```



The cache lives at `~/.cache/tidy3d/simulations` by default. Clearing it frees the corresponding **Hidden Files** space immediately.

This does **not** delete your cloud simulations. Your tasks in [Folders](https://tidy3d.simulation.cloud/folders) are unaffected — only the local copies used to skip re-runs are removed.

You can also control whether the cache is used at all, set a size limit, or change its directory via `td.config.local_cache`. See: [How do I control the local cache in Tidy3D?](https://docs.flexcompute.com/projects/tidy3d/en/latest/faq/docs/faq/how-do-i-control-the-local-cache-in-tidy3d.html)



## Important to know

- **Notebook storage ≠ cloud workspace storage.** Hidden Files are on your notebook environment's disk. Simulations you've submitted live separately in your cloud [Folders](https://tidy3d.simulation.cloud/folders) and are governed by your cloud workspace quota.
- **It's safe to clear the Tidy3D cache.** It only affects re-run speed for identical simulations; nothing about your results, notebooks, or cloud data is lost.
- **It's not always safe to delete other dotfolders.** `.jupyter/` and `.local/` hold settings; `.git/` holds your version history. Prefer the `clear_cache()` approach above unless you know what a folder is.
