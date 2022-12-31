## gnssIR_api
This bash script runs the archive section of the https://gnss-reflections.org API.
For instructions, make sure the script is executable (chmod +x gnssIR_api) and type its name:

### Inputs
There are three required inputs: 

* station name (4 characters, lower case) 
* year 
* day of year

An easy example (for a good reflection site in New Mexico):
  
* ./gnssIR_api p038 2019 152

The rest of the inputs to the script are optional, but can be set if you have a preference:
  
*   -e1 and -e2 for elevation angles in degrees (defaults are 5 and 25)
*   -azim1 and -azim2 are azimuth angles in degrees (defaults are 0 and 360)
*   -freq can be L1, L2, L2C, L5, L1L2CL5, or L1L2. Default is L1
*   -h1 and -h2 are reflector height constraints in meters. Defaults are currently 0.5 and 7 meters
  
For the archive section of the API, if you would like to run multiple days use the optional -doy_end flag
  
### Quality Control Parameters:
  
*   -amp sets the periodogram peak required. The default is 6 - but it is not the right value for all receivers. You can set it to zero if you like.

*   -pk2noise is peak size related to background noise ratio. Default is now at 4 - but you can certainly make that lower, 3.5 for snow or ice. For water, 3 is a good number to start with.

Please see http://gnss-reflections.org/overview for more information.

### Daily Average Reflector Height

This information is stored in the outputdir defined in the script (the default directory is solutions) 
as station_RH_all.csv. It uses the azimuth angle restrictions provided by the user.
All reflector height estimates are stored in daily files within the outputdir folder. 
This purpose of this option is to make it easy for the snow/ice communities that are mostly
interested in daily values.  This option is NOT appropriate for tides, though it would be 
appropriate for lake monitoring.
  
### Additional Information
For the archives, the RINEX file must be archived at the locations recognized by the web app.  Currently that 
means the low-rate sections of UNAVCO, SOPAC, and SONEL.
  
If you want to upload a RINEX file, you have to follow the rules of the API, which are spelled out
on https://gnss-reflections.org

### Examples:
  
* Niwot Ridge, Colorado - L2C is in the RINEX files.  This was a great snow site.

     ./gnssIR_api nwot 2019 300 -freq L1L2 -h1 0.5 -h2 8 -azim1 45 -azim2 240 -e1 5 -e2 20
  
* Phoenix, Ross Ice Shelf, Antarctica - L2C is in the RINEX files. No azimuth restrictions needed because ... it is Antarctica

     ./gnssIR_api phnx 2019 300 -freq L1L2 -h1 0.5 -h2 8
  
* Lake Superior, Canada - L1 only as this site does not support modern GPS signal tracking. Azimuth restrictions have been added to emphasize the water reflections of interest.

     ./gnssIR_api mchn 2019 205 -azim1 50 -azim2 210 -h1 2.5 -h2 8 -pk2noise 3.5 -archive sopac
  
* Island Park, Idaho - good snow site. Would be better if you had access to L2C. Contact UNAVCO.

     ./gnssIR_api p360 2019 100  -pk2noise 3.5
  
* If you happened to have a RINEX file with the name p0013640.20o.gz, then you could upload it directly as:

     ./gnssIR_api p001 2020 364 -rinex p0013640.20o.gz 

Kristine M. Larson

https://kristinelarson.net

December 29, 2022

