# modifying-nc-files
 In this repository I have added a text file where I have given specific instructions how to re-grid and crop out the netCDF files

This is a text file about how to modify the netCDF (nc) files into the relevant way for this study. I am going to explain step by step what I am doing and I am doing this only in my terminal (macOS).

1. I am going to convert the nc files of NOAA CDR from polar-stereographic grid to EASE2 grid so it matches the grid as OSI-SAF’s dataset. Put all the commands I am writing now into your terminal step-by-step.


>  cdo

> cd <path_to_your_files>

>  cdo -remapnn,ice_conc_nh_ease2-250_cdr-v2p0_20190101-20191231.nc -setgrid,seaice_conc_daily_nh_f17_20190101_v03r01.nc seaice_conc_daily_nh_2019_v04r00.nc noaa_on_osi_2019.nc


Structure:
cdo -remapnn,<OSI-SAF 2019 nc file> -setgrid,<NOAA any v3 nc file> <NOAA 2019 nc file> <newly gridded NOAA output file>


This will change the grid system of the nc file of NOAA’s (seaice_conc_daily_nh_2019_v04r00.nc) into OSI-SAF’s grid system (osi_2019.nc). The version 3 file from NOAA (seaice_conc_daily_nh_f17_20190101_v03r01.nc) is needed for executing the command. This file does not have any purpose in the data of the files.


2. Do this same command for all of the files. For example, with the 2020 files it would look like this:


>  cdo -remapnn,ice_conc_nh_ease2-250_cdr-v2p0_20200101-20201231.nc -setgrid,seaice_conc_daily_nh_f17_20190101_v03r01.nc seaice_conc_daily_nh_2020_v04r00.nc noaa_on_osi_2020.nc

And so on…


3. Now I will crop out the regions that the study focuses on. Those are: Baffin Bay, the northwest of Ellesmere Island, Beaufort Sea and Laptev Sea.


Baffin Bay

I picked out a region in Baffin Bay on the 2016 file. To crop out that specific part, you need to put these commands in your terminal:

>  cdo

> cd <path_to_your_files>

> cdo -sellonlatbox,-70,-65,72,74 ice_conc_nh_ease2-250_cdr-v2p0_20160101-20161231.nc baffin_bay_osi_2016.nc


Structure:
cdo -sellonlatbox,lon1,lon2,lat1,lat2 <OSI-SAF or NOAA nc file name> <output nc file>

Do the same thing for all the years.


The northwest of Ellesmere Island:

 > cd <path_to_your_files>

> cdo -sellonlatbox,-117,-125,78,84 ice_conc_nh_ease2-250_cdr-v2p0_20160101-20161231.nc ellesmere_osi_2016.nc



Beaufort Sea:

Laptev Sea:
