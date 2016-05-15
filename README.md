# Mapproxy Dockerfile

This will build a [docker](http://www.docker.com/) image that runs [mapproxy
](http://mapproxy.org).

## Getting the image

There are various ways to get the image onto your system:


The preferred way (but using most bandwidth for the initial image) is to
get our docker trusted build like this:


```
docker pull openseamap/mapproxy
```

To build the image yourself without apt-cacher (also consumes more bandwidth
since deb packages need to be refetched each time you build) do:

```
docker build -t openseamap/mapproxy git://github.com/aAXEe/mapproxy-docker
```


# Run

To run a mapproxy container do:

```
docker run --name "mapproxy" -p 8080:8080 -d -t openseamap/mapproxy
```

Typically you will want to mount the mapproxy volume, otherwise you won't be
able to edit the configs:

```
mkdir mapproxy
docker run --name "mapproxy" -p 8080:8080 -d -t -v `pwd`/mapproxy:/mapproxy openseamap/mapproxy
```

The first time your run the container, mapproxy basic default configuration
files will be written into ``./mapproxy``. You should read the mapproxy documentation
on how to configure these files and create appropriate service definitions for
your WMS services. Then restart the container to activate your changes.

The cached wms tiles will be written to ``./mapproxy/cache_data``.

**Note** that the mapproxy containerised application will run as the user that
owns the /mapproxy folder.

The webservic will be available at:

```
http://localhost:8080/
```
