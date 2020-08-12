# map-header

Fancy Website banner rotating a street-network on dark background map

<img src="https://firebasestorage.googleapis.com/v0/b/hydrocode-website.appspot.com/o/public%2Fhydrocode_brand.png?alt=media&token=3ec35465-9c1c-48a1-8d3f-2c93549a4ffb" width="400">

## Overview

This repo is a quick example of how an actual mapbox map can be used as a website banner. THe code is in a single HTML file and the data is downloaded from overpass-turbo, as is.
If you want to use it in production, there are several measures that should be taken:

1. decrease the size of the `geojson` file (it's about 30MB) - see below
2. split the code into several files
3. add information and context to the map. e.g. create a `geojson` of hoverable places or open popups with information by timing functions
4. split the street network into two (or more) files, to more easily apply styling to it (e.g. keep the smaller streets static and transition the `line-blur` only for bigger streets)
5. if you use it - please attribute us
6. keep in mind that the data is ODbL licensed

## decreasing file size

1. only the `LineString` geometries in the `export.geojson` is visualized, but there is still `Polygon` and `Point` features contained. Remove them.
2. You can consider to exclude very small streets like lanes or pedestrian
3. Use shapely or QGis to union geometries of same Type. This decreases the feature count, which is turn makes mapbox a bit faster
4. you can also tidy up the `properties` - here only the `highway` attribute is used
5. many `highway` types are treated the same way, e.g. `motorway` and `primary`. You can merge these as well.
