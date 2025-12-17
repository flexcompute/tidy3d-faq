---
title: How to Manage Storage and Download Simulation Data in Tidy3d?
date: 2025-12-17 16:23:41
enabled: true
category: "About Tidy3D"
---
When running simulations in Tidy3D, your cloud storage may eventually reach its limit. This FAQ explains how to clean up space, download your data, and manage simulation files using both the GUI and the Python API.

---

## **How do I free up storage space so I can continue running simulations?**

You must delete older simulation files from your cloud storage. You can do this either through the GUI or the Python API.

---

## **How do I delete simulations using the GUI?**

1. Go to your **Workspace**:  
   <https://tidy3d.simulation.cloud/folders>

2. Select the simulation files you want to remove.

3. A bar will appear at the bottom of the page with options to **download** or **delete** the selected files.

4. Download anything you want to keep, then delete the files to free up cloud storage.

---

## **How do I download and delete simulations using the Python API?**

### **Download simulation data**

Use the method:  
<i>web.download(task_id)</i>  
API documentation:  
<https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.download.html>

### **Delete simulation data**

Use the method:  
<i>td.web.delete(task_id)</i>  
API documentation:  
<https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.delete.html>

### **List recent simulations**

Use:  
<i>web.get_tasks</i>  
Documentation:  
<https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.get_tasks.html>

### **Automatically delete old simulations**

Use:  
<i>web.delete_old</i>  
Documentation:  
<https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.delete_old.html>

---

## **Where is simulation data saved when I run a simulation?**

When you run a simulation using:  
<i>web.run</i>  
Documentation:  
<https://docs.flexcompute.com/projects/tidy3d/en/latest/api/_autosummary/tidy3d.web.api.webapi.run.html>

Two things happen:

1. The data is saved **automatically in the cloud** in the folder specified by the <i>folder_name</i> argument.
2. A copy is saved **locally on your machine** at the path specified by the <i>path</i> argument.

---

## **What should I do if I still have issues?**

If you're unsure which files are taking up space or need help managing your tasks, feel free to contact Tidy3D Support.

---

