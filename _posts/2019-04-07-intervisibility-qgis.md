---
layout: post
published: true
title: 'Intervisibility analysis in QGIS: an archaeological tutorial'
tags:
  - qgis
  - QGIS visibility plugin
---
Intervisibility analysis tests the potential for visual connection between two observers. I say potential because visibility on landscape scale is often the question of a myriad factors (distance, atmosphere, signal quality etc...). Visibility analysis in GIS is usually taking into account only the terrain (plus solid buildings) and tests whether a visual connexion would be blocked by the terrain. The choice of distance limit and other factors will depend upon the problem in question. For instance, wind turbines will be seen over longer distances in the night, because of those strong, ugly lights.

![19-04-plugin_main.JPG]({{site.baseurl}}/figures/19-04-plugin_main.JPG)
*Intervisibility module of QGIS Visibility analysis plugin.*

## Towers BC

Anyway, instead of wind turbines, let’s examine the intervisibility problem on a prettier example, ancient Greek towers. Ancient Greeks were busy tower-builders: hundreds of stone-built towers, mostly dating to 5th and 4th century BC, still survive in the Greek countryside. These constructions were square or circular in plan and typically under 10 meters in diameter. Full elevation is very rarely preserved. Several structures that subsist to near-original height indicate a general trend of the height as the double of the diameter (Young 1956). The function of the towers seems to have been primarily defensive and strategic, they would have provided refuge from potential robber/pirate attacks and allow visual control over the landed property.
 
 ![19-04-tower_andros.jpg]({{site.baseurl}}/figures/19-04-tower_andros.jpg)
*Agios Petros tower on Andros Island (www.kastra.eu)*


Before constructing such a tower, which is a serious investment of time and resources, one would need to consider carefully its placement: close to farmed land but in low position, or on a hill with a good view, in view with other towers, but perhaps hidden from potential attack route, etc. These questions just beg for a GIS analysis... Intervisibility analysis can inform us on the potential for visual communication between towers. One can suppose that in the case of an imminent danger some kind of visual signalling across the countryside would have been more than welcome.

## Analysis 

My case study will be the island of Sifnos (Siphnos) which, for reasons still debated, was furnished with a dense network of towers (see below for references). The database I’m using may not meet all scientific standards (here goes my disclaimer), but it’s more than enough for this tutorial. 

Lines of sight between towers will be analysed in QGIS with the [Visibility analysis plugin]( www.zoran-cuckovic.from.hr/QGIS-visibility-analysis/). The module requires two sets of points, one that stores the points of origin of intervisibility lines and the other that stores the target points. In case when sources are the same as targets, we can specify the same file as both the source and the target.

Some users were having difficulties to grasp the parameters involved. Note that in many, if not most cases we use the same set of locations for both signal emitters and receivers. The term intervisibility implies that the relationship is reciprocal between two locations: observers are, in turn, signal emitters. However, the visibility relationship is not necessarily reciprocal in the real world. We can see a tower at a distance only if we see a good portion of it, say at least the top five meters. Let's assume that Greek towers typically measured 15 metres; in this case we will test intervisibility for the height of 10 meters. But this does not apply to the observer who is comfortable at the top of a tower: see figure below. Therefore we need two parameters for each tower, its observation height and its target height. 

![19-04-towers.jpg]({{site.baseurl}}/figures/19-04-towers.jpg)
*The problem of reciprocity (images from www.svgrepo.com/svg/140937/tower).*

The same would apply if we were using two different datastes, for instance the view of towers from villages. Towers would become targets and only their target height would be taken into account (here, 10 meters); likewise, villages would become observers and only their observer height would be needed.  

These parameters are specified through the *Create viewpoints* module. (Note that you can vary the value for each point by editing the associated data table.). Other parameters, such as radius of analysis etc. shouldn’t need further explanation. **Important** : target height does not refer to view targets, here other towers. Indeed, every tower can have its specific height when acting as a target. Therefore target height and observer height parameters always refer to the same structre which may act **as** observer point or **as** view target.   

![19-04-create_points.jpg]({{site.baseurl}}/figures/19-04-create_points.jpg)

The elevation model used is [EU DEM](www.eea.europa.eu/data-and-maps/data/eu-dem) with approx. 30 metres horizontal resolution. The QGIS visibility analysis plugin [**will only work on rasters projected in a metric coordinate system**](/2020/wgs/).

The result of the analysis is intriguing (figure below). We can notice several closely knit communities, but very bad connection with the most important settlement on the eastern coast of the island. Did tower builders care more about their neighbours than about the city folk? I will leave you to ponder on what this could mean…

![19-04-intervisibility_all.jpg]({{site.baseurl}}/figures/19-04-intervisibility_all.jpg)
*Intervisibility connections between towers (circles) and the urban area of Siphnos polis (orange square).*

Let us return to technical issues. I’ve stressed that intervisibility is not reciprocal, and our analysis used different heights for observers and visual targets. We can expect, then, to have some non-reciprocal connexions where only one tower can be seen at 10 meters height, the other being visible at 15 metres. In order to filter out such broken links we will need to test whether each Source-Target pair could be matched with corresponding Target-Source pair. This can be done with a moderately advanced SQL query that can be specified under general properties of QGIS layers. The magic formula is:
``` 
"Source" || '-' || "Target" IN 
(Select "Target" || '-' || "Source" from Intervisibility)
```
where “Intervisibility” is layer name in my particular project. “Source” and “Target” are column names in the algorithm output. To join field values I’m using the magic sign `||` which somehow works in QGIS (it does not appear among the proposed SQL operators). There is a spearator between values `'-'` to prevent misidentification (345 can be produced as 3 || 45 or 34 || 5).
Note that we are using a so-called subquery, specified by a Select statement in parentheses. Subqueries are usually arcane, but this one should be simple enough to grasp. Essentially, the engine is forced to scan the entire table for each Source-Target pair, searching for its potential match. This may become computationally heavy for large datasets (but *really* large).
 
 ![19-04-layer_properties.JPG]({{site.baseurl}}/figures/19-04-layer_properties.JPG)
*Query builder under Layer properties in QGIS.*
 
Now we can have a clean map with reciprocal relationships only. But, these are all in pairs, which is not useful any more since one-directional connections were eliminated. If your Source and Target IDs are numerical, as assigned automatically by the Visibility module, then the filtering is straightforward. For each connection pair, one ID will be greater than the other (there should be no duplicate IDs, obviously), so we can just append to our filter `Source > Target `: 
```
"Source" || '-' || "Target" IN 
(Select "Target" || '-' || "Source" from Intervisibility)
AND "Source" > "Target"
```

![19-04-query.JPG]({{site.baseurl}}/figures/19-04-query.JPG)
*Final layer query.*

And finally, to select broken links we simply modify the criteria to NOT IN. We need to remove the direction filter because we cannot know in advance which direction will be broken. 
``` 
"Source" || '-' || "Target" NOT IN 
(select "Target" || '-' ||  "Source" from Intervisibility)
```

![19-04-intervisibility_broken.jpg]({{site.baseurl}}/figures/19-04-intervisibility_broken.jpg)
*Broken intervisibility links (non-reciprocal).*

Happy mapping!

## NB
The SQL subquery may not work with temporary layers or even shapefiles. Save the intervisibilty network in GeoPackage format to avoid the issue: 
![19-04-geopackage.jpg]({{site.baseurl}}/figures/19-04-geopackage.jpg)

## Sources & bibliography 

Ashton, N. G. and Pantazoglou, E. Th. (1991): *Siphnos: ancient towers BC*. Athens. [I used their database.]

Davies G. N. (1998): *Economic Geography of the Ancient Greek Countryside: A re-examination of monumental rural sites on the island ofSiphnos.* PhD, Oxford.

Young, J. H. (1956) : Ancient Towers on the Island of Siphnos. *American Journal of Archaeology*, vol. 60/1, pp. 51-55.

The Towers of Sifnos: [www.sifnos-towers.gr](https://www.sifnos-towers.gr/en.html) [This is a new website with an updated database.]
