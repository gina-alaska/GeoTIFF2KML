# GeoTIFF to KMZ/KML demo

This is a quick demo to show how to generate a KMZ/KML from a GeoTIFF that crosses the international date line

## Requirements

* gdal 1.10+
* Terminal window/command line interface

## Instructions

We will start by turning the following GeoTIFF into a KML

http://feeder.gina.alaska.edu/npp-gina-alaska-truecolor-images/2016_02_07_22_18_jd_38

1. Make the project space
```
mkdir kmldemo
```

2. Get the image
```
wget http://feeder.gina.alaska.edu/dragonfly/2016/02/07/14_53_37_99_npp.16038.2218_M05_M04_M03_I01.tif
gdalinfo 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.tif
```

3. make the left kml
```
gdalwarp -of VRT -rb -wo SOURCE_EXTRA=25 -rb -t_srs epsg:4326 -te 160 40 180 80 -tr 0.016433853738702 0.016433853738702 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.tif 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.left.vrt
```
```
mkdir left
```
```
gdal_translate -of KMLSUPEROVERLAY -a_nodata 0 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.left.vrt left/left.kmz -co format=png
```

4. make the right kml
```
gdalwarp -of VRT -rb -wo SOURCE_EXTRA=25 -rb -t_srs epsg:4326 -te -180 40 -120 80 -tr 0.016433853738702 0.016433853738702 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.tif 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.right.vrt
```
```
mkdir right
```
```
gdal_translate -of KMLSUPEROVERLAY -a_nodata 0 14_53_37_99_npp.16038.2218_M05_M04_M03_I01.right.vrt right/right.kmz -co format=png
```

5. open the kmls in GoogleEarth
