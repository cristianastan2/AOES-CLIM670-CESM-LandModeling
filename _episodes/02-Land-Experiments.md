---
title: "Land Model Experiments"
questions:
- "Land Model Experiments"
objectives:
keypoints:
- ""
---

## 3 Experiments with Land Model

### Basic CLM5 Experiment

Run the land model (CLM5) with satellite phenology (SP) at 1 deg horizontal resolution for 5-days

`compset:` I2000Clm50Sp

`resolution:` f09_g17_gl4

Namelist changes:

* daily averages (hist_nhtfrq)

* make history files contain 5-days + initialization day (hist_mfilt)

How do we check that we did not make and mistakes in our namelist?

Configuration changes:

./xmlchange --subgroup case.run JOB_WALLCLOCK_TIME=0:15:00

What does this do?

When the run is complete, where will the land history data be located?


## Understand Differences between Land Compsets

Run the same configuration as above, but with a different compset.

`compset`: IHistClm50BgcCrop

Where would I look up this difference between this compset and the previous one?

How could I compare the configuration differences?


When this run and the previous run are complete, compare teh leaf and stem area index (`TLAI`,`TSAI`), transpiration and canopy and ground evaporation (`FCTR`,`FCEV`,`FGEV`). 

What is the reason for the differences based on what you know about the different compsets?

## Understand Inputs for CLM

Look at the `lnd_in` namelist for the first experiment. 

Find the parameter file specified by the `paramfile` namelist item.

We will look at this file in Jupyter, specifically the variable `rholvis`.  This is the visible leaf reflectance for each plant functional type (pft).  Its the amount of visible radiation reflected by the different types of plants.  

This is an input file for the land model. We will change the values in this file and see what that does to the model simulation.

What is plant functional type #4?

What is the `rholvis` values for plant functional type #4?

Create a new file which changes the visible leaf reflectance of plant functional type #4 (tropical broadleaf evergreen tree) to 0.4.  

What have we done to this?

Write the data to a netcdf file.

Create a new experiment exactly like the first one, but change it to use your new file.

Where would you change this?

Compare the history output against that generated in the first experiment.  Here's a nice tool for making that comparison:

~~~
ncdiff hist_exp1 hist_exp2.nc hist_diff.nc
~~~
{: .language-bash}

Now you can ncview the `hist_diff.nc` file to see the differences.

How did this change impact your experiment?  Some variables to compare: `FSRVD`,`FSRVI`,`FSR`,`FSA`,`FSH`,`FCSTR`,`TV`,`TSA`).  Use `ncdump` to get their full name and units.

