---
layout: post
title: "Homebrew QGIS, clean batch"
description: "i finally got QGIS *HEAD* running on OS X"
category: QGIS
tags: [Homebrew, QGIS, OS X]
---
{% include JB/setup %}

Embarassing to admit how long it took me get there - but I finally was able to build QGIS *HEAD* on OS X from Homebrew. If you have a relatively vanilla system - you can *probably* follow Ragi Burhum's post [here](http://blog.burhum.com/post/36080548777/getting-qgis-working-on-homebrew).

I wanted to provide a couple tips for those of you without the cleanest systems - maybe you have a mix of library installs from Homebrew & other sources. Start by cleaning up any Kyngchaos,etc libs/frameworks and ensure they're only installed nicely from Homebrew. You might want to run `brew cleanup` and `brew doctor` … handle any issues if needed. I forked below from [Brian Mount](https://twitter.com/brian_mount/status/299590722271723520) - a little nudge in the right direction. Symlink your Homebrew libs similarly:

	sudo mkdir -p /Library/Frameworks/GDAL.framework/Versions/1.9/
	sudo ln -s /usr/local/lib/libgdal.dylib /Library/Frameworks/GDAL.framework/Versions/1.9/GDAL
	sudo mkdir -p /Library/Frameworks/PROJ.framework/Versions/4/
	sudo ln -s /usr/local/Cellar/proj/4.8.0/lib/libproj.dylib /Library/Frameworks/PROJ.framework/Versions/4/PROJ
	# did not work: sudo ln -s `pwd`/libgeos.dylib /Library/Frameworks/GEOS.framework/Versions/3/GEOS
	# did work:
	# $PWD is /usr/local/Cellar/geos/3.3.6/lib
	sudo ln -s `pwd`/libgeos_c.1.dylib /Library/Frameworks/GEOS.framework/Versions/3/GEOS
	sudo mkdir -p /Library/Frameworks/SQLite3.framework/Versions/3/
	sudo ln -s /usr/local/Cellar/sqlite/3.7.15/lib/libsqlite3.0.8.6.dylib /Library/Frameworks/SQLite3.framework/Versions/3/SQLite3`

Covering all bases, I also ran `brew rm --force --purge` on PyQt, Qwt, SIP and Python. Then reinstalled.

$PYTHONPATH is set for `/usr/local/lib/python2.7/site-packages`

Hopefully then, `brew install qgis --HEAD --with-postgis --with-grass` will work for you - like it **finally** did me.
