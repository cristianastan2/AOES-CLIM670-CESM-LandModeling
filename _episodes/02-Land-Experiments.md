---
title: "Land Model Experiments"
questions:
- "Land Model Experiments"
objectives:
keypoints:
- ""
---

# 3 Experiments with Land Model

## Basic CLM5 Experiment

Run the land model (CLM5) with satellite phenology (SP) at 1 deg horizontal resolution for 5-days

`compset:` I2000Clm50Sp

`resolution:` f09_g17_gl4

> ## Compset information
>
> How can I find out what this compset means?
>
> https://www.cesm.ucar.edu/models/cesm2/config/2.1.1/compsets.html
>
>
{: .challenge}


#### Namelist changes:

* daily averages (hist_nhtfrq)

* make history files contain 5-days + initialization day (hist_mfilt)

> ## Namelists
> 
> What file do I make namelist change in for the land?
>
> What is the command for checking namelists?
>
> Where is it run from?
>
{: .challenge}

#### Configuration changes:

Reduce the wallclock time.

~~~
./xmlchange --subgroup case.run JOB_WALLCLOCK_TIME=0:15:00
~~~
{: .language-bash}

> ## History Files
>
> When the run is complete, where will the land history data be located?
>
>
{: .challenge}


## Understand Differences between Land Compsets

Run the same configuration as above, but with a different compset.

`compset`: IHistClm50BgcCrop

> ## Compsets
>
> Where would I look up this difference between this compset and the previous one?
>
>
> Which files in my two cases should I compare to see
>
>
{: .challenge}

> ## Finding create_newcase setup
>
>  What file tells me the create_newcase command I ran for the first exeriment?
>
>
{: .challenge}

When this run and the previous run are complete, compare teh leaf and stem area index (`TLAI`,`TSAI`), transpiration and canopy and ground evaporation (`FCTR`,`FCEV`,`FGEV`). 

> ## Interpreting output
>
> What is the reason for the differences based on what you know about the different compsets?
>
>
{: .challenge}

## Understand Inputs for CLM

Look at the `lnd_in` namelist for the first experiment. 

> ## Resolved Namelists
>
> Where is the `lnd_in` namelist file for the first experiment located?
> 
>
{: .challenge}

Find the parameter file specified by the `paramfile` namelist item.

> ## What is the name of the file?
>
>
{: .challenge}

This file defines specific information about each of the plant function types in CLM.  This is an important input file for the land model.

We will look at this file in Jupyter, specifically the variable `rholvis`.  This is the visible leaf reflectance for each plant functional type (pft).  Its the amount of visible radiation reflected by the different types of plants.  

> ## How do I launch Jupyter (or Python in general) from Cheyenne?
>
> 
{: .challenge}

This is an input file for the land model. We will change the values in this file and see what that does to the model simulation.

> ## Looking at data in .nc files
>
> What is plant functional type #4?
>
> What is the `rholvis` value for plant functional type #4?
>
{: .challenge}

## Creating new input files
>
> Create a new file which changes the visible leaf reflectance of plant functional type #4 (tropical broadleaf evergreen tree) to 0.4.  
>
> Write the data to a netcdf file.
>
{: .challenge}

Create a new experiment exactly like the first one, but change it to use your new file.

> ## Cloning
>
> What command creates an exact replica of another experiment?
>
> Where is that command run from?
>
{: .challenge}

## Changing Land Input files
>
> Where would you change this so your new case will 
> find the new input file?
>
{: .challenge}

#### While the model is building...

* What do you think this change did?

* What do you expect the the impact to be?

Compare the history output against that generated in the first experiment.  Here's a nice tool for making that comparison:

~~~
ncdiff hist_exp1 hist_exp2.nc hist_diff.nc
~~~
{: .language-bash}

Now you can ncview the `hist_diff.nc` file to see the differences.

> ## How did this change impact your experiment? 
>
> Some variables to compare: `FSRVD`,`FSRVI`,`FSR`,`FSA`,`FSH`,`FCSTR`,`TV`,`TSA`).  Use `ncdump` to get their full name and units.
> 
> Was the impact what you expected?
>
{: .challenge}

