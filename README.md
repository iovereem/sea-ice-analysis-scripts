# sea-ice-analysis-scripts

README.TXT

Sea Ice Dataset: Sea Ice Concentrations from Nimbus-7 SMMR and DMSP SSM/I-SSMIS Passive Microwave Data, Version 1

This is daily data of sea ice concentration for the entire Arctic region, as generated from brightness temperature data from remotely-sensed passive microwave signals. The dataset is processd to provide a continuous record over the lifespan of several passive microwave sensors (the Nimbus-7 Scanning Multichannel Microwave Radiometer (SMMR), the Defense Meteorological Satellite Program (DMSP) -F8, -F11 and -F13 Special Sensor Microwave/Imagers (SSM/Is), and the DMSP-F17 Special Sensor Microwave Imager/Sounder (SSMIS). The data are provided in the polar stereographic projection at a grid cell size of 25 x 25 km.
Sea ice concentrations is defined as the fraction, or percentage, of ocean area covered by sea ice

Downloaded binary files for all years from:
https://nsidc.org/data/NSIDC-0051/versions/1

Data citation: Cavalieri, D. J., C. L. Parkinson, P. Gloersen, and H. J. Zwally. 1996, updated yearly. Sea Ice Concentrations from Nimbus-7 SMMR and DMSP SSM/I-SSMIS Passive Microwave Data, Version 1. Boulder, Colorado USA. NASA National Snow and Ice Data Center Distributed Active Archive Center. doi: https://doi.org/10.5067/8GQ8LZQVL0VL. [Accessed November 11th, 2020].


Processing scripts

Used three matlab scripts in sequence  to generate the posted data: 

findFirstLastOWV1(y,69,219,'./NSIDCseaIce', 0.15)

This script runs through all binary data files downloaded from NSIDC for each day of a given year. It calculates for a given X,Y location
1)	what is the sea ice concentration (SIC), 
2)	writes this to a daily sea ice concentration file, tagge by the year and location coordinates
3)	The script also keeps track of the first day sea ice concentration falls below a given concentration threshold 15% coverage and the last day before sea ice refreezes to concentrations higher than 15% coverage. The period in between is defined as the duration of open water. 
4)	Last day of open water, LOW, First Day of Open Water, FOW.


function FindSicOWMultipleYears(startYear,endYear)

This simply calls the previous script repetitively for all years defined by the start year and end year. 

Once all files are written into the output directory, one can run a short script to get summary statistics of open water duration, first day of open water and last day of open water: 

function WriteSummary_OWDays(startYear,endYear,SICthreshold) 


Location determination: 
https://nsidc.org/data/polar-stereo/ps_grids.html

Install and compile with gnu compiler three fortran codes available from NSIDC
called locate.for, mapxy.for, mapll.for
These allow you to type in a latitude, longitude coordinate (as positive values) and return the grid I,J locations. 

For the Canning delta I used: 70.05, 145.3 which becomes 70.05, 214.7

Run in terminal: 
./locate

It returns grid cell 69,219
