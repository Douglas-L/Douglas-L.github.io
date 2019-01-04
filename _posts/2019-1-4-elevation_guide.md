---
layout: post
title: How to look up elevation given longitude and latitude
author: "Douglas Lee"
categories: journal
tags: [howto, api, location, fires]
image: elevation_tif.png
visible: 1
---


In my search for features with signal during my fire classification project,I wanted to look up a location's elevation given its longitude and latitude. Finding an easy and free way to do so took longer than expected, so I am writing this post to help others in need of elevation data. 

If you only have a few locations to look up, I recommend the [Elevation Point Query Service](https://nationalmap.gov/epqs/), provided by the United States Geological Survey (USGS). However, querying at scale is not so easy. The EPQS actually offers a batch query API but it is currently limited to only 500 queries. Google offers an API for elevation, but it makes no sense to pay for publicly available information. 

After searching for other ways to access the elevation data, I found that the USGS also releases elevation data with 100-meter resolution as TIFF files. These files require a specific utility to retrieve the elevation at the given coordinates. The [gdallocationinfo utility](https://www.gdal.org/gdallocationinfo.html) is a command line tool that "provide a mechanism to query information about a pixel given its location in one of a variety of coordinate systems." 

The Elevation maps for the US can be found at the following links: [the conterminous US](https://www.sciencebase.gov/catalog/item/581d0539e4b08da350d52552), [Alaska](https://www.sciencebase.gov/catalog/item/581d0539e4b08da350d52557), [Hawaii](https://www.sciencebase.gov/catalog/item/581d053ae4b08da350d5255b), and [Puerto Rico](https://www.sciencebase.gov/catalog/item/581d053ae4b08da350d5255f).

# Using gdallocation utility
```
Usage: gdallocationinfo [--help-general] [-xml] [-lifonly] [-valonly]
                        [-b band]* [-overview overview_level]
                        [-l_srs srs_def] [-geoloc] [-wgs84]
                        [-oo NAME=VALUE]* srcfile [x y]
```

Using the tool in command line is straightforward. Simply fill in the filepath to your TIFF file for "srcfile", the longitude in degrees for "y", and the latitude in degrees for "x". 

Don't forget to specify "-wgs84", which lets the tool know you're using longitude and latitude coordinates, and "-valonly", which makes the tool return the elevation in meters at the location. 

To use the gdallocationinfo utility within python, the [os.popen](https://docs.python.org/3/library/os.html#os.popen) function opens a pipe to the command line. From there, you read in the result and you're done!
```
def gen_get_elevation(lon, lat, tiff_path):
    return os.popen(f'gdallocationinfo -valonly -wgs84 {tiff_path} {lon} {lat}').read().strip()
```
            
Read() returns the value as a string. In the case it can't find the given coordinates, as in the case of looking up Hawaii coordinates in the Alaska TIFF,for example, it will simply return an empty string, so try to make sure you're looking in the right TIFF file. 

Thank you for reading. Check out how I use the gdallocation in my [Elevation notebook on Github](https://github.com/Douglas-L/Predicting_Wildfire_Size/blob/master/Fires2_3_Elevation.ipynb). Credits to [user20408](https://gis.stackexchange.com/questions/118397/store-result-from-gdallocationinfo-as-variable-in-python) for pointing out the popen function. 

