# [DEPRECATED] Buildpack: Geo

The Geo buildpack is deprecated. This is no longer officially supported, but feel free to fork it to make it work on the most recent stacks.

This is a [Scalingo
buildpack](https://doc.scalingo.com/platform/deployment/buildpacks/intro) that
installs the Geo/GIS libraries [GDAL](https://www.gdal.org/),
[GEOS](https://trac.osgeo.org/geos/) and [PROJ](https://proj4.org/).

It can be used to get
[GeoDjango](https://docs.djangoproject.com/en/2.1/ref/contrib/gis/) or
[RGeo](https://github.com/rgeo/rgeo) running on Scalingo.

## Usage

### Enable PostgreSQL PostGIS Extension

PostgreSQL includes [several extensions](https://doc.scalingo.com/databases/postgresql/extensions). PostGIS is an extension to
handle geospatial data. After adding a PostgreSQL database to your application,
you can enable the PostGIS extension with:

```bash
$ scalingo --app my-app pgsql-console
> CREATE EXTENSION postgis;
```

Next step is to install the libraries Django requires to manipulate these data.

### Install Geospatial Libraries

These libraries are **proj**, **geos** and **gdal**. Considering that they are
not used commonly, they are not included in our default environment so you need
to install them at deployment time.

#### Usage of the geo-buildpack

To deploy an application with these libraries you need to use an additional
buildpack along with the default Python buildpack.

  Reminder: a buildpack is a piece of software able to detect and install
  dependencies of a given technology. More information about [Scalingo's buildpacks](https://doc.scalingo.com/platform/deployment/buildpacks/intro).

Create a `.buildpacks` file at the root of your project with the following content to make use of the [multi buildpack](https://doc.scalingo.com/platform/deployment/buildpacks/multi):

```text
https://github.com/Scalingo/geo-buildpack
https://github.com/Scalingo/python-buildpack
```

#### Deploy your application

```bash
git add .buildpacks
git commit -m "Use geo-buildpack as long as python-buildpack"
git push scalingo master
```

Then you'll see in your deployment output:

```text
=====> Downloading Buildpack: https://github.com/Scalingo/geo-buildpack.git
=====> Detected Framework: geos/gdal/proj
       Using geos version: 3.4.2
       Using gdal version: 1.11.1
       Using proj version: 4.8.0_1
       ...
```

## Default Versions

The buildpack will install the following version by default:

GDAL - 2.4.0</br>
GEOS - 3.7.2</br>
PROJ - 5.2.0</br>

You can change the version of each library that will be installed by setting the
`GDAL_VERSION`, `GEOS_VERSION` or `PROJ_VERSION` config variables.
