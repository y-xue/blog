---
layout: page
title: Ray Cluster Setup
---

Ray needs to import local modules on each node of the cluster. If I define a class (e.g. in Data_loader.py) and an application imports Data_loader module, I need to make sure this file is shared by all nodes in the cluster. 