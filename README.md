# gnssIR_api
This bash script runs the archive section of the https://gnss-reflections.org API.
For instructions, make sure the script is executable and type its name:
* ./gnssIR_api

## Inputs
There are three required inputs: 

* station name (4 characters, lower case), year, and day of year.


An easy example (for a good reflection site in New Mexico):
  
* ./gnssIR_api p038 2019 152

The rest of the inputs to the script are optional, but can be set if you have a preference:
  
*   -e1 and -e2 for elevation angles in degrees (defaults are 5 and 25)
*   -azim1 and -azim2 are azimuth angles in degrees (defaults are 0 and 360)
*   -freq can be L1, L2, L2C, L5, or L1L2. Default is L1
*   -h1 and -h2 are reflector height constraints in meters. Defaults are 0.5 and 7 meters
  
If you would like to run multiple days, use the optional -doy_end flag
  
## Quality Control Parameters:
  
*   -amp sets the periodogram peak required. The default is 8 - but it is not the right value for all receivers.

*   -pk2noise is peak size related to background noise ratio. Four is the default and good for most snow work

## Daily Average Reflector Height
This information is stored in the outputdir defined in the script (the default directory is solutions) 
as station_RH_all.csv. It uses the azimuth angle restrictions provided by the user.
All reflector height estimates are stored in daily files within the outputdir folder. 
This purpose of this option is to make it easy for the snow/ice communities that are mostly
interested in daily values.  This option is NOT appropriate for tides, though it would be 
appropriate for lake monitoring.
  
## Additional Information
The RINEX file must be archived at the locations recognized by the web app.  Currently that 
means the low-rate sections of UNAVCO, SOPAC, CDDIS, and SONEL.
  
The API creates a task queue on the site that hosts the site (heroku). 
This task usually takes from 5 to 10 seconds to complete. This bash script 
queries the API every two seconds to see if the task is completed.
It saves the results (and tells you where those are being saved). If you would 
prefer a different location for your results, change the outputdir variable in 
the bash script. The daily set of reflector height
outputs includes everything that meets certain quality control metrics.
  
This script does not check for all possible errors by users. Further, it is not the right place
to look for documentation on the API or for questions about what a reflector height is. For that
you need to look at the FAQ/overview section at https://gnss-reflections.org
I am working on adding access to the RINEX uploader in this script, but it is not ready
for distribution as yet.

## Examples:
  
* Niwot Ridge, Colorado - L2C is in the RINEX files.  Great snow site.

     ./gnssIR_api nwot 2019 300 -freq L1L2 -h1 0.5 -h2 8 -azim1 45 -azim2 240 -e1 5 -e2 20
  
* Phoenix, Ross Ice Shelf, Antarctica - L2C is in the RINEX files. No azimuth restrictions needed because ... it is Antarctica

     ./gnssIR_api phnx 2019 300 -freq L1L2 -h1 0.5 -h2 8
  
* Lake Superior, Canada - L1 only as this site does not support modern GPS signal tracking. Azimuth restrictions have been added to emphasize the water reflections of interest.

     ./gnssIR_api mchn 2019 205 -azim1 50 -azim2 210 -h1 2.5 -h2 8 -pk2noise 3.5
  
* Island Park, Idaho - good snow site. Would be better if you had access to L2C. Contact UNAVCO.

     ./gnssIR_api p360 2019 100  -pk2noise 3.5
  
## Where are the soil moisture results?
The API does not support soil moisture applications at this time.

Kristine M. Larson

https://kristinelarson.net

