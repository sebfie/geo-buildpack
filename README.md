# [DEPRECATED] Buildpack: Geo

The Geo buildpack is deprecated. This is no longer officially supported, but feel free to fork it to make it work on the most recent stacks.

This is a [Scalingo
buildpack](https://doc.scalingo.com/platform/deployment/buildpacks/intro) that
installs the Geo/GIS libraries [GDAL](https://www.gdal.org/),
[GEOS](https://trac.osgeo.org/geos/) and [PROJ](https://proj4.org/).

It can be used to get
[GeoDjango](https://docs.djangoproject.com/en/2.1/ref/contrib/gis/) or
[RGeo](https://github.com/rgeo/rgeo) running on Scalingo.

Usage
-----

 It is meant to be used in conjunction with other buildpacks as part of a
 [multi-buildpack](https://doc.scalingo.com/platform/deployment/buildpacks/multi).

Ensure that the Geo buildpack is the first buildpack on your list of buildpacks:

```
$ cat .buildpacks
https://github.com/Scalingo/geo-buildpack
https://github.com/Scalingo/python-buildpack
```

Default Versions
----------------

The buildpack will install the following version by default:

GDAL - 2.4.0</br>
GEOS - 3.7.2</br>
PROJ - 5.2.0</br>

You can change the version of each library that will be installed by setting the
`GDAL_VERSION`, `GEOS_VERSION` or `PROJ_VERSION` config variables.
