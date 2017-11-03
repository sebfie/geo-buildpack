Buildpack: geo
=====================

This is a [Scalingo buildpack](http://doc.scalingo.com/buildpacks) that
vendors main geo/gis libraries like geos, proj and gdal.

It is meant to be used in conjunction with other buildpacks as part of a
[multi-buildpack](http://doc.scalingo.com/buildpacks/multi).

Usage
-----

Example usage:

    $ scalingo env-set BUILDPACK_URL=https://github.com/Scalingo/multi-buildpack.git

    $ cat .buildpacks
    https://github.com/Scalingo/geo-buildpack
    https://github.com/Scalingo/ruby-buildpack


Testing
-------

For Geo Django:

```python
>>> from django.contrib.gis import gdal
>>> gdal.HAS_GDAL
True
```

For rgeo:

```ruby 
>>> require 'rgeo'
>>> RGeo::CoordSys::Proj4.supported?
=> true
>>> RGeo::Geos.supported?
=> true
```
