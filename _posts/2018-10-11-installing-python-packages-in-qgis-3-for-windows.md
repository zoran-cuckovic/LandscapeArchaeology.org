---
layout: post
author: Zoran
categories:
  - Spatial analysis &amp; GIS
date: 'Thu Oct 11 2018 20:02:55 GMT+0200 (heure d’été d’Europe centrale)'
guid: 'https://landscapearchaeology.org/?p=331'
id: 331
permalink: /2018/installing-python-packages-in-qgis-3-for-windows/
tags:
  - qgis
title: Installing Python packages in QGIS 3 (for Windows)
published: true
---

Python is in the heart of QGIS (or in the guts if you prefer), which enables us to use tons of third party Python libraries. In Linux systems, QGIS will use the main Python installation, but in Windows things get more complicated. QGIS has it's own Python, which means we end up with various Pythons on our machines...

This is how to proceed in QGIS 3.x in Windows (I work on Win. 7)
1. Open OSGeo4W shell (packed with QGIS in the start menu)
1b. [older versions only]  Type ```py3_env```. This should print paths of your QGIS Python installation. 
2. Use Python's ```pip``` to install the library of your choice: ```python -m pip install my-crazy-library```

[![](/wp/wp-content/uploads/2018/10/Capture.png)](/wp/wp-content/uploads/2018/10/Capture.png)

Remark 1: I don't need to open the shell as administrator -- but this could solve some problems if the program starts complaining about permissions, or if you are not the only user. 

Remark 2: Large packages may _break interent connection_. In order to prevent this, you can force the routine to wait longer using ```--default-timeout=1000``` flag. This would give : ```python -m pip --default-timeout=1000 install my-crazy-library```

**Option 2**

Packages can also be installed directly from within Python, but that is not the preferred approach. Open QGIS Python console (under Plugins >> Python Console) and type: 

```
>> import pip

>> pip.main(['install', 'my-package-name'])

```
Note that the arguments are given as a list [...] of 'strings'.
