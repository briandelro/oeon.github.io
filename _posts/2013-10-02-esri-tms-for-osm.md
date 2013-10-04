---
layout: post
title: "Esri TMS for OSM"
description: "tracing against Esri tiles"
category: openstreetmap
tags:
- tms
- openstreetmap
- esri
- arcgis server
published: true
---
{% include JB/setup %}

<a href="http://www.flickr.com/photos/j03lar50n/10079654826/" title="Untitled by j03lar50n, on Flickr"><img src="http://farm4.staticflickr.com/3832/10079654826_f9d47d0bc0.jpg" width="500" height="375" alt="Untitled"></a>  

---

I wanted to log my efforts connecting to an Esri ArcGIS Server (AGS) raster layer / TMS-like tile service from JOSM and iD OpenStreetMap Editors. I didn't see much material out-there, specifically for AGS, so maybe someone else will find this useful.

[Previously](http://joelarson.com/work/2013/09/10/cuttin-tiles/), I wrote about cutting tiles for consumption via TMS…one method to share that gdal2tiles output is via Amazon S3. For example, a US Standard (region) bucket named '*tile-demo*' connection URL for iD is: `https://s3.amazonaws.com/tile-demo/{z}/{x}/{-y}.png`. Thank goodness one can pass `-y` instead of running a script to [rename TMS layout to Google layout](https://gist.github.com/oeon/6801339) on 6 million tiles.  
  
<p><a href="http://www.flickr.com/photos/j03lar50n/10079499413/" title="tiles_z19size_total by j03lar50n, on Flickr"><img src="http://farm8.staticflickr.com/7301/10079499413_728377cf85_o.jpg" width="237" height="73" alt="tiles_z19size_total"></a></p>

Another option you may encounter is tiles available from an ArcGIS tile cache (is that the right term?). Here's how I got there, provided your source also publishes the imagery under an appropriate license & in web mercator, EPSG 3857.

REST resource URL: `http://gis.yourcounty.ca.gov/arcgis/rest/services`

for iD: `http://gis.yourcounty.ca.gov/arcgis/rest/services/Aerials/2014_1_FT_AERIAL/MapServer/tile/{z}/{y}/{x}`

for JOSM, use 'zoom' instead of 'z': `http://gis.yourcounty.ca.gov/arcgis/rest/services/Aerials/2014_1_FT_AERIAL/MapServer/tile/{zoom}/{y}/{x}`

*I didn't need to specify image filetype in the URL* e.g. *.jpg* / *.png*

So, if you have something like that available in your area - and it's better quality/resolution that Bing .. try out those custom sources templates as base imagery during your OpenStreetMap editing.

**EDIT**: Ian Dees replied, "Another option is to use the WMS endpoint that ships with all MapServer instances with JOSM's WMS code. OSM US can also proxy" see [https://twitter.com/iandees/status/386150404737622016](https://twitter.com/iandees/status/386150404737622016)
