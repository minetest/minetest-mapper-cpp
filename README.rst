Minetest Mapper C++
===================

.. image:: https://travis-ci.org/minetest/minetestmapper.svg?branch=master
    :target: https://travis-ci.org/minetest/minetestmapper

Minetestmapper generates an overview image from a Minetest map.

A port of minetestmapper.py to C++ from https://github.com/minetest/minetest/tree/master/util.
This version is both faster and provides more features than the now deprecated Python script.

Requirements
------------

* libgd
* sqlite3
* LevelDB (optional)
* hiredis (optional)
* Postgres libraries (optional)

on Debian:
^^^^^^^^^^

	sudo apt install libgd-dev libsqlite3-dev libleveldb-dev libhiredis-dev libpq-dev

on openSUSE:
^^^^^^^^^^^^

        sudo zypper install gd-devel sqlite3-devel leveldb-devel hiredis-devel postgresql-devel postgresql-server-devel

Windows
^^^^^^^
Minetestmapper for Windows can be downloaded here: https://github.com/minetest/minetestmapper/releases

After extracting the archive, minetestmapper can be invoked from cmd.exe:
::

	cd C:\Users\yourname\Desktop\example\path
	minetestmapper.exe --help

Compilation
-----------

::

    cmake . -DENABLE_LEVELDB=1
    make -j$(nproc)

Usage
-----

`minetestmapper` has two mandatory paremeters, `-i` (input world path)
and `-o` (output image path).

::

    ./minetestmapper -i ~/.minetest/worlds/my_world/ -o map.png


Parameters
^^^^^^^^^^

bgcolor:
    Background color of image, e.g. ``--bgcolor '#ffffff'``

scalecolor:
    Color of scale marks and text, e.g. ``--scalecolor '#000000'``

playercolor:
    Color of player indicators, e.g. ``--playercolor '#ff0000'``

origincolor:
    Color of origin indicator, e.g. ``--origincolor '#ff0000'``

drawscale:
    Draw scale(s) with tick marks and numbers, ``--drawscale``

drawplayers:
    Draw player indicators with name, ``--drawplayers``

draworigin:
    Draw origin indicator, ``--draworigin``

drawalpha:
    Allow nodes to be drawn with transparency (e.g. water), ``--drawalpha``

extent:
    Don't output any imagery, just print the extent of the full map, ``--extent``

noshading:
    Don't draw shading on nodes, ``--noshading``

noemptyimage:
    Don't output anything when the image would be empty, ``--noemptyimage``

min-y:
    Don't draw nodes below this y value, e.g. ``--min-y -25``

max-y:
    Don't draw nodes above this y value, e.g. ``--max-y 75``

backend:
    Override auto-detected map backend; supported: *sqlite3*, *leveldb*, *redis*, *postgresql*, e.g. ``--backend leveldb``

geometry:
    Limit area to specific geometry (*x:z+w+h* where x and z specify the lower left corner), e.g. ``--geometry -800:-800+1600+1600``

zoom:
    Apply zoom to drawn nodes by enlarging them to n*n squares, e.g. ``--zoom 4``

colors:
    Override auto-detected path to colors.txt, e.g. ``--colors ../minetest/mycolors.txt``

scales:
    Draw scales on specified image edges (letters *t b l r* meaning top, bottom, left and right), e.g. ``--scales tbr``

exhaustive:
    | Select if database should be traversed exhaustively or using range queries, available: *never*, *y*, *full*, *auto*
    | Defaults to *auto*. You shouldn't need to change this, but doing so can improve rendering times on large maps.
    | For these optimizations to work it is important that you set ``min-y`` and ``max-y`` when you don't care about the world below e.g. -60 and above 1000 nodes.
