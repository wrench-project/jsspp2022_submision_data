# jsspp2022_submission_data

This repository contains data, scripts, and code for making the research in a JSSPP'22 submission reproducible.

## Simulator code

The simulator is hosted in [another repository](XXX). All experiments are conducted with the simulator with commit tag XXXX. A docker image is provided in which the simulator has been installed in `/usr/local/bin/scheduling_with_simulations_imulator`.

    - Install everytingm AND mongo in the DOCKER

## Workflow JSON files

All JSON workflow description files, which are [WfCommons instances](https://wfcommons.org/instances) used in this work are available in the `workflows` directory.

## Scripts to run all simulations

Scripts to run all simulations are available in the `run_scripts` directory. They require that a Mongo daemon run locally, so that simulation output can be stored in a database.

## Simulation raw output

Simulation raw output is available as a Mongo database dump in the `mongo_db_dump` directory 

## Scripts to extract simulation output from Mongo

Scripts to extract and summarize simulation output data from the Mongo database are available in the `extract_scripts` directory, which also contains a number of `*.dict` files with the extracted output. These scripts require that a Mongo daemon run locally that has been fed the database dump in directory `mongo_db_dump` directory. 

## Scripts to plot/analyze the simulation output

Scripts to plot/analyze extracted simulation output data are available in the `plot_scripts` directory.  These scripts take as input the `*dict` files available in the `extract_scripts` directory.
