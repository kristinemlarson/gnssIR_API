# gnssIR_api
This bash script runs the archive section of the https://gnss-reflections.org API.
There are three required inputs: station name, year, and day of year.
To try it out, make sure the script is executable and type:
  
./gnssIR_api p038 2019 152
  

# Inputs
The rest of the inputs are optional, but can be set if you have a preference:
  
   -e1 and -e2 for elevation angles in degrees (defaults are 5 and 25)
  
   -azim1 and -azim2 are azimuth angles in degrees (defaults are 0 and 360)
  
   -freq can be L1, L2, L2C, L5, or L1L2. Default is L1
  
   -h1 and -h2 are reflector height constraints in meters. Defaults are 0.5 and 7 meters
  
If you would like to run multiple days, use the optional -doy_end flag
  
# Quality Control Parameters:
  
   -amp sets the periodogram peak required. The default is 8 - but it is not the right value for all receivers.

   -pk2noise is peak size related to background noise ratio. Four is the default and good for most snow work

# Daily Average Reflector Height
This information is stored in the outputdir defined in the script (the default directory is solutions) as
station_RH_all.csv
  
# Additional Information
The RINEX file must be archived at the locations recognized by the web app.  Currently that 
is the low-rate sections of UNAVCO, SOPAC, CDDIS, and SONEL.
  
My API creates a task queue on the site that hosts my API (heroku). This usually takes from 5 to 10 seconds to
complete. This bash script queries the API every two seconds to see if it has completed.
It saves the results (and tells you where those are being saved). If you would prefer a different
location for your results, change the outputdir variable in the bash script. The daily set of reflector height
outputs includes everything that meets certain quality control metrics.
  
If you input azimuth constraints, the API will output a daily average within those
azimuths with additional QC. This is meant to make it easy for the snow/ice communities.
This option is NOT appropriate for tides, though it would be appropriate for lake monitoring.
  
This script does not check for all possible errors by users. Further, it is not the right place
to look for documentation on the API or for questions about what a reflector height is. For that
you need to look at the FAQ/overview section at https://gnss-reflections.org
I am working on adding access to the RINEX uploader in this script, but it is not ready
for distribution as yet.
  

Kristine M. Larson
https://kristinelarson.net
https://gnss-reflections.org
