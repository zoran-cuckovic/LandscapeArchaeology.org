---
author: Zoran
categories:
- Spatial analysis &amp; GIS
date: 2018-05-25 16:57:53
guid: https://landscapearchaeology.org/?p=246
id: 246
layout: post
permalink: /2018/polar-diagram/
tags:
- qgis
title: Polar (circular) diagram
---

Orientation of geographic features can be an important piece of information, for instance when studying ancient field systems or analysing geological formations. The problem comes when we try to summarise such data graphically . Standard histograms are not ideal because they cut through the continuous distribution - one cannot easily understand the relationship between the beginning and the end of the diagram (which should stick together). Polar diagram is what we need, but it cannot be made without some fiddling around.

<a href="https://3.bp.blogspot.com/-L93oFU5wimQ/WgbxUnriF5I/AAAAAAAAA2A/9Odg-QlGj3o7X84AZlXDWaiV9La2ugElACLcBGAs/s1600/2017-11-Polar-graph.jpg"><img src="https://3.bp.blogspot.com/-L93oFU5wimQ/WgbxUnriF5I/AAAAAAAAA2A/9Odg-QlGj3o7X84AZlXDWaiV9La2ugElACLcBGAs/s400/2017-11-Polar-graph.jpg" alt="" /></a>

There already exists a plugin called <a href="https://plugins.qgis.org/plugins/LineDirectionHistogram/">Line direction histogram</a> that does the job quite fine. However, QGIS comes with great matplotlib python library for data visualisation (windows version at least) which can be tweaked in all imaginable ways (colours, offsets etc.). The following script is simply passing data to matplotlib, **directions have to be pre-calculated beforehand**, i.e. you should have a table field with calculated directions. The same applies for the raster version - it works on an aspect raster where each cell stores an angular value. 

The scripts can be downloaded at [https://github.com/zoran-cuckovic/QGIS-scripts](https://github.com/zoran-cuckovic/QGIS-scripts) (search for "polar histogram").
