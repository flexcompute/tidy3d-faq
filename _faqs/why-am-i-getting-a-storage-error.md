---
title: Why am I getting an Exceed Storage error?
date: 2026-03-09 15:55:24
enabled: true
category: "About Tidy3D"
---
Tidy3D licenses have three different storage/memory limits:

-   Hosted notebook environment RAM: in our [hosted notebook environment](https://tidy3d.simulation.cloud/notebook), this is the hosted environment's working memory used to store data and objects while the notebook is running. This is found in the bottom left corner of the notebook page next to "Mem."
-   Hosted notebook environment storage: also in our hosted notebook environment, this is the hosted environment's is the disk space available, for storage of the notebook files themselves, simulation data run from the environment, additional benchmarking data, etc. This can also be found in the bottom left corner of the notebook page next to "Storage."
-   Cloud storage: this is where all simulation data associated to the account is stored. All data computed by Tidy3D simulations on the account is saved here. This can be found at one's [account page](https://tidy3d.simulation.cloud/account). This page can also be found by clicking the user icon in the upper right corner of the Tidy3D [account home page](https://tidy3d.simulation.cloud/home) and selecting "My Plan and Storage".

To clear cloud storage, it is recommended to use Tidy3D's [web.delete()](https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.delete.html) function. Tidy3D can also delete all data older than a specified number of days. Alternatively, users can manually inspect and delete tasks on the Tidy3D account [workspace](https://tidy3d.simulation.cloud/folders).

Flexcompute also provides options to upgrade to more storage and memory. Please contact us at support@flexcompute.com if interested.